---
layout: post
title:  "HttpInvoker over OAuth2 with Spring Boot 2.2"
author: stephen
categories: [ OAuth2, Spring Security, Spring Framework, RMI, Swing ]
image: assets/images/6.jpg
---
Ok, so `HttpInvoker` may not be the what the hipsters are using (it's been around since 2003 or so) but there are still plenty of Java desktop applications out there communicating over RMI or EJB that could use a security boost.

If you've got a desktop app communicating to a server over RMI, how are you authorizing the calls? If the app is on the end-user's machine, how can you keep any secret auth information? 
* username/password? - exposed
* static token? - exposed
Although obfuscation mechanisms can be used, any text can be extracted from the jar on the persons machine.

So how can you keep a secret on a public application? You can't. But OAuth2 authorization_code grant can be used in combination with PKCE to obtain short-lived access tokens for a specific user to securely communicate with server endpoints.

How can we do this?

Let's build on baeldungs http-invoker tutorial. First create an OAuth2-aware WebClient:

{% highlight java %}
@Configuration
public class WebClientConfig {

	@Bean
	WebClient webClient(ClientRegistrationRepository clientRegistrationRepository, OAuth2AuthorizedClientRepository authorizedClientRepository) {
		ServletOAuth2AuthorizedClientExchangeFilterFunction oauth2 = new ServletOAuth2AuthorizedClientExchangeFilterFunction(clientRegistrationRepository, authorizedClientRepository);
		oauth2.setDefaultOAuth2AuthorizedClient(true);
		return WebClient.builder()
				.apply(oauth2.oauth2Configuration())
				.build();
	}
}
{% endhighlight %}

Create a custom `WebClientHttpInvokerRequestExecutor` that will send your requests using the OAuth2-aware `WebClient`:

{% highlight java %}
public class WebClientHttpInvokerRequestExecutor extends AbstractHttpInvokerRequestExecutor {

    private final WebClient webClient;

    public WebClientHttpInvokerRequestExecutor(WebClient webClient) {
        this.webClient = webClient;
    }

    @Override
    protected RemoteInvocationResult doExecuteRequest(HttpInvokerClientConfiguration config, ByteArrayOutputStream baos) throws IOException, ClassNotFoundException {
        InputStreamResource inputStreamResource = this.webClient
                .post()
                .uri(config.getServiceUrl())
                .header(HTTP_HEADER_CONTENT_TYPE, CONTENT_TYPE_SERIALIZED_OBJECT)
                .syncBody(new ByteArrayResource(baos.toByteArray()))
                .exchange()
                .flatMap(response -> response.bodyToMono(InputStreamResource.class))
                .block();

        return readRemoteInvocationResult(inputStreamResource.getInputStream(), config.getCodebaseUrl());
    }
}
{% endhighlight %}

Ensure your security configuration uses Spring Security's OAuth2 Client and uses OAuth2 Login...

{% highlight java %}
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

	@Override
	protected void configure(HttpSecurity http) throws Exception {
		http
			.authorizeRequests()
				.anyRequest().authenticated()
				.and()
			.formLogin()
				.and()
			.oauth2Login()
				.and()
			.oauth2Client();
	}
}
{% endhighlight %}


Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: http://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/