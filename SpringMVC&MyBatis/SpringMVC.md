## SpringMVC

#### Spring 框架的 7 个模块
![Spring 框架](https://www.ibm.com/developerworks/cn/java/wa-spring1/spring_framework.gif "Spring 框架模块图")

#### SpringMVC是什么？

>Spring Web MVC是一种基于Java的实现了Web MVC设计模式的请求驱动类型的轻量级Web框架，即使用了MVC架构模式的思想，将web层进行职责解耦，基于请求驱动指的就是使用请求-响应模型，框架的目的就是帮助我们简化开发。

#### SpringMVC运行流程图

![Spring 流程图](../resources/SpringMVC流程.png "Spring MVC流程图")

##### 核心架构的具体流程步骤如下：

- 首先用户发送请求——>DispatcherServlet，前端控制器收到请求后自己不进行处理，而是委托给其他的解析器进行处理，作为统一访问点，进行全局的流程控制；
- DispatcherServlet——>HandlerMapping， HandlerMapping将会把请求映射为HandlerExecutionChain对象（包含一个Handler处理器（页面控制器）对象、多个HandlerInterceptor拦截器）对象，通过这种策略模式，很容易添加新的映射策略；
- DispatcherServlet——>HandlerAdapter，HandlerAdapter将会把处理器包装为适配器，从而支持多种类型的处理器，即适配器设计模式的应用，从而很容易支持很多类型的处理器；
- HandlerAdapter——>处理器功能处理方法的调用，HandlerAdapter将会根据适配的结果调用真正的处理器的功能处理方法，完成功能处理；并返回一个ModelAndView对象（包含模型数据、逻辑视图名）；
- ModelAndView的逻辑视图名——> ViewResolver， ViewResolver将把逻辑视图名解析为具体的View，通过这种策略模式，很容易更换其他视图技术；
- View——>渲染，View会根据传进来的Model模型数据进行渲染，此处的Model实际是一个Map数据结构，因此很容易支持其他视图技术；
- 返回控制权给DispatcherServlet，由DispatcherServlet返回响应给用户，到此一个流程结束。

#### Spring MVC优势

- 清晰的角色划分
  - 前端控制器（DispatcherServlet）
  - 请求到处理器映射（HandlerMapping）
  - 处理器适配器（HandlerAdapter）
  - 视图解析器（ViewResolver）
  - 处理器或页面控制器（Controller）
  - 验证器（Validator）
  - 命令对象（Command  请求参数绑定到的对象就叫命令对象）
  - 表单对象（Form Object 提供给表单展示和提交到的对象就叫表单对象）

- 分工明确，而且扩展点相当灵活，可以很容易扩展

- 由于命令对象就是一个POJO，无需继承框架特定API，可以使用命令对象直接作为业务对象

- 和Spring 其他框架无缝集成，是其它Web框架所不具备的

- 可适配，通过HandlerAdapter可以支持任意的类作为处理器

- 可定制性，HandlerMapping、ViewResolver等能够非常简单的定制

- 功能强大的数据验证、格式化、绑定机制

- 利用Spring提供的Mock对象能够非常简单的进行Web层单元测试



  #### [DispatcherServlet.doDispatch](https://www.cnblogs.com/lj95801/p/4961456.html)
>所有的http请求都会交给DispatcherServlet类的doDispatch方法进行处理

```java
protected void doDispatch(HttpServletRequest request,
            HttpServletResponse response) throws Exception {

        // processedRequest是经过checkMultipart方法处理过的request请求
        HttpServletRequest processedRequest = request;
        /**
         * Handler execution chain, consisting of handler object and any handler
         * interceptors. Returned by HandlerMapping's HandlerMapping.getHandler
         * method. 看看HandlerExecutionChain类的属性就很清楚了：
         *
          public class HandlerExecutionChain {

                  private final Object handler; //这个就是和该请求对应的handler处理方法

                 //里面记录了所有的(any handler interceptors)和该请求相关的拦截器
                  private HandlerInterceptor[] interceptors;

                  private List<HandlerInterceptor> interceptorList;

                  private int interceptorIndex = -1;

                  //...
          }
         *
         */
        HandlerExecutionChain mappedHandler = null;
        boolean multipartRequestParsed = false;

        WebAsyncManager asyncManager = WebAsyncUtils.getAsyncManager(request);

        try {
            ModelAndView mv = null;
            Exception dispatchException = null;

            try {
                processedRequest = checkMultipart(request);
                multipartRequestParsed = (processedRequest != request);

                // Determine handler for the current request.Return a handler
                // and any interceptors for this request.
                /*
                 * 得到的mappedHandler包含一个请求的handler处理方法以及与该请求相关的所有拦截器
                 *
                 * DispatcherServlet.getHandler方法会在底层调用HandlerMapping.getHandler方法
                 * ，这个方法中会遍 历DispatcherServlet中的private List<HandlerMapping>
                 * handlerMappings链表，找到能够处理当前 request请求的第一个HandlerMapping实例并返回：
                 *
                  protected HandlerExecutionChain getHandler(HttpServletRequest request) throws Exception {
                      for (HandlerMapping hm : this.handlerMappings) {
                              HandlerExecutionChain handler = hm.getHandler(request);
                              if (handler != null) {
                                     return handler;
                              }
                      }
                      return null;
                  }
                 *
                 */
                mappedHandler = getHandler(processedRequest);
                // 如果没有找到和该请求相对应的mappedHandler，那么就会直接返回，并应答noHandlerFound异常
                if (mappedHandler == null || mappedHandler.getHandler() == null) {
                    noHandlerFound(processedRequest, response);
                    return;
                }

                // Determine handler adapter for the current request.
                /*
                 * HandlerAdapter: 它是一个接口public interface HandlerAdapter
                 * 看看源码上的说明：The DispatcherServlet accesses all installed
                 * handlers through this interface, meaning that it does not
                 * contain code specific to any handler type.
                 *
                 * 从后面的源码看出，在使用@RequestMapping注解标注handler方法的时候，获取到的是HandlerAdapter的
                 * RequestMappingHandlerAdapter实现类的一个对象。
                 *
                 * 可以看看DispatcherServlet.getHandlerAdapter方法的定义，这个对理解上回很有帮助，我们会发现
                 * ，getHandlerAdapter 方法和上面提到的getHandler方法一样都是寻找第一个可用的作为返回结果：
                 *
                 *
                  protected HandlerAdapter getHandlerAdapter(Object handler) throws ServletException {
                     //this.handlerAdapters的定义是 private List<HandlerAdapter> handlerAdapters
                         for (HandlerAdapter ha : this.handlerAdapters) {
                              if (ha.supports(handler)) {
                                   return ha;
                              }
                         }
                         throw new ServletException("No adapter for handler [" + handler +
                                 "]: The DispatcherServlet configuration needs to include a HandlerAdapter that supports this handler");
                  }
                 *
                 */
                HandlerAdapter ha = getHandlerAdapter(mappedHandler
                        .getHandler());

                // Process last-modified header, if supported by the handler.
                String method = request.getMethod();
                boolean isGet = "GET".equals(method);
                if (isGet || "HEAD".equals(method)) {
                    long lastModified = ha.getLastModified(request,
                            mappedHandler.getHandler());
                    if (logger.isDebugEnabled()) {
                        logger.debug("Last-Modified value for ["
                                + getRequestUri(request) + "] is: "
                                + lastModified);
                    }
                    if (new ServletWebRequest(request, response)
                            .checkNotModified(lastModified) && isGet) {
                        return;
                    }
                }

                // Apply preHandle methods of registered interceptors.
                /*
                 * 会调用所有注册拦截器的preHandle方法，如果preHandle方法的返回结果为true，则会继续执行下面的程序，
                 * 否则会直接返回。
                 *
                 * 分析一下HandlerExecutionChain.applyPreHandle方法的源码 ：
                  boolean applyPreHandle(HttpServletRequest request, HttpServletResponse response) throws Exception {
                         //从上面的HandlerExecutionChain定义处可以看见有个interceptors，还有一个interceptorList。不知道有什么区别？？！
                         HandlerInterceptor[] interceptors = getInterceptors();
                         //如果已经注册有拦截器，则遍历拦截器
                         if (!ObjectUtils.isEmpty(interceptors)) {
                             for (int i = 0; i < interceptors.length; i++) {
                                 HandlerInterceptor interceptor = interceptors[i];
                                 //如果注册拦截器的preHandle方法返回一个false，则该applyPreHandle方法就会返回false，从而在doDispatcher中的代码就不会往下执行了
                                 if (!interceptor.preHandle(request, response, this.handler)) {

                                     //这个方法要注意，它会调用所有已经成功执行的拦截器的afterCompletion方法，而且是反序调用的过程，可以分析triggerAfterCompletion
                                     //的源代码，主要是利用interceptorIndex反减的方式实现的。下面是源码的英文注释：
                                     //Trigger afterCompletion callbacks on the mapped HandlerInterceptors.
                                      //Will just invoke afterCompletion for all interceptors whose preHandle invocation
                                      //has successfully completed and returned true.
                                     triggerAfterCompletion(request, response, null);
                                     return false;
                             }
                                 //没成功执行一个拦截器的preHandle方法，其interceptorIndex就会增加1；原始值为-1。
                                  this.interceptorIndex = i;
                             }
                         }
                         return true;
                     }
                 *
                 *
                 *  顺带看看triggerAfterCompletion的源代码，很容易理解为什么拦截器的afterCompletion方法是反序执行的：
                 *    void triggerAfterCompletion(HttpServletRequest request, HttpServletResponse response, Exception ex)
                             throws Exception {

                        HandlerInterceptor[] interceptors = getInterceptors();
                        if (!ObjectUtils.isEmpty(interceptors)) {
                            for (int i = this.interceptorIndex; i >= 0; i--) {
                                HandlerInterceptor interceptor = interceptors[i];
                                try {
                                    interceptor.afterCompletion(request, response, this.handler, ex);
                                }
                                catch (Throwable ex2) {
                                    logger.error("HandlerInterceptor.afterCompletion threw exception", ex2);
                                }
                            }
                        }
                    }
                 *
                 *
                 */
                if (!mappedHandler.applyPreHandle(processedRequest, response)) {
                    return;
                }

                // Actually invoke the handler.
                /*
                 * 在这个函数里面会真正的执行request请求相对于的handler方法，可以想象：在真正调用方法之前还会有很多的
                 * 先前处理。在这里仅仅是分析出大概的代码执行流程，其细节的部分在后面的单独模块源码分析的时候做详细的讲解。
                 * 上面讲解到HandlerAdapter是一个接口：public interface HandlerAdapter，那么必然会有很多
                 * 中实现类，在采用注解@RequstMapping的方式标注handler的情况下，ha.handle方法会在底层调用具体的
                 * HandlerAdapter类实现方法RequestMappingHandlerAdapter.handleInternal
                 *
                 * 分析一下RequestMappingHandlerAdapter.handleInternal的源代码：
                      protected ModelAndView handleInternal(HttpServletRequest request,
                        HttpServletResponse response, HandlerMethod handlerMethod) throws Exception {
                        //好像是看control的类定义处是否使用了@SessionAttributes注解，checkAndPrepare方法有什么作用？？？
                        if (getSessionAttributesHandler(handlerMethod).hasSessionAttributes()) {
                            // Always prevent caching in case of session attribute management.
                            checkAndPrepare(request, response, this.cacheSecondsForSessionAttributeHandlers, true);
                        }
                        else {
                            // Uses configured default cacheSeconds setting.
                            checkAndPrepare(request, response, true);
                        }

                        // Execute invokeHandlerMethod in synchronized block if required.
                        // 这里是个值得注意的地方，synchronizeOnSession的值默认为false，如果通过某个方法使得其为true，那么request对应的handler
                        // 将会被放在同步快中进行处理。在什么时机下，使用什么方法才能将其设置为true呢？？？
                        if (this.synchronizeOnSession) {
                            HttpSession session = request.getSession(false);
                            if (session != null) {
                                Object mutex = WebUtils.getSessionMutex(session);
                                // 将handler放在同步块中处理
                                synchronized (mutex) {
                                    return invokeHandleMethod(request, response, handlerMethod);
                                }
                            }
                        }
                        //在invokeHandleMethod中会①将所有标注有@ModelAttrib的方法都执行一遍，②调用invokeAndHandle(webRequest, mavContainer)
                        //方法，在这里面调用handler方法，③最后调用getModelAndView(mavContainer, modelFactory, webRequest)方法的到ModelAndView。
                        //invokeHandleMethod这个方法还有很多东西要分析，留在后面。
                        //从上面的③我们可以看出，无论handler采用哪种模型化处理方式，最后都是将结果转化为ModelAndView
                        return invokeHandleMethod(request, response, handlerMethod);
                    }
                 */
                mv = ha.handle(processedRequest, response,
                        mappedHandler.getHandler());

                if (asyncManager.isConcurrentHandlingStarted()) {
                    return;
                }

                applyDefaultViewName(request, mv);
                /*
                 * 调用request相关的拦截器的postHandle方法，注意，这个也是反序调用的。看看源代码：
                 *
                  void applyPostHandle(HttpServletRequest request, HttpServletResponse response, ModelAndView mv) throws Exception {
                        HandlerInterceptor[] interceptors = getInterceptors();
                        if (!ObjectUtils.isEmpty(interceptors)) {
                            //注意，这里也是反序执行，而且是所有成功执行了的postHandle拦截器
                            for (int i = interceptors.length - 1; i >= 0; i--) {
                                HandlerInterceptor interceptor = interceptors[i];
                                //这里传入的参数中有mv，也就是说，我们是有办法在拦截器的postHandle方法中修改已经返回的mv
                                interceptor.postHandle(request, response, this.handler, mv);
                            }
                        }
                    }
                 */
                mappedHandler.applyPostHandle(processedRequest, response, mv);
            } catch (Exception ex) {
                dispatchException = ex;
            }
            processDispatchResult(processedRequest, response, mappedHandler,
                    mv, dispatchException);
        } catch (Exception ex) {
            triggerAfterCompletion(processedRequest, response, mappedHandler,
                    ex);
        } catch (Error err) {
            triggerAfterCompletionWithError(processedRequest, response,
                    mappedHandler, err);
        } finally {
            if (asyncManager.isConcurrentHandlingStarted()) {
                // Instead of postHandle and afterCompletion
                if (mappedHandler != null) {
                    mappedHandler.applyAfterConcurrentHandlingStarted(
                            processedRequest, response);
                }
            } else {
                // Clean up any resources used by a multipart request.
                if (multipartRequestParsed) {
                    cleanupMultipart(processedRequest);
                }
            }
        }
    }
```
>doDispath方法中处理http请求的流程

![doDispath流程](https://images2015.cnblogs.com/blog/808517/201511/808517-20151113104035619-604403700.png "doDispath流程")
