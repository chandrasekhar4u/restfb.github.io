{% highlight java %}
// You'll want to initialize the bridge just once at app startup.
// In a webapp, a good place to do this is ContextLoaderListener#contextInitialized()
SLF4JBridgeHandler.install();

try {
  FacebookClient facebookClient = new DefaultFacebookClient();

  // You'll notice that logging statements from this call are bridged from java.util.logging to Log4j
  User user = facebookClient.fetchObject("btaylor", User.class);

  // ...and of course this goes straight to Log4j
  logger.debug(user);
} finally {
  // Make sure to tear down when you're done using the bridge
  SLF4JBridgeHandler.uninstall();
}
{% endhighlight %}