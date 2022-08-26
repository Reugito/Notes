#Importent Things Related Development

1. Fixing host injection through proxy server in api
  a. defing this in WebSecurityConfigurerAdapter configurations
  
     @Override
  public void configure(WebSecurity web) throws Exception {
      StrictHttpFirewall firewall = new StrictHttpFirewall();
      firewall.setAllowedHostnames(hostname -> hostname.equals(domainHostName));;
      web.httpFirewall(firewall);
  }
  
  b. Refer 
  
  https://github.com/spring-projects/spring-security/issues/4310
  https://security.stackexchange.com/questions/186826/host-header-injection-attack-with-spring-boot-embedded-tomcat
