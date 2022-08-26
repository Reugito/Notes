#Importent Things Related Development

1. Fixing host injection through proxy server in api
  a. defing this in WebSecurityConfigurerAdapter configurations
  
     @Override
  public void configure(WebSecurity web) throws Exception {
      StrictHttpFirewall firewall = new StrictHttpFirewall();
      firewall.setAllowedHostnames(hostname -> hostname.equals(domainHostName));;
      web.httpFirewall(firewall);
  }
