# Notes

import java.util.Properties;

public static void main(String[] args) throws Exception {
    SpringApplication application = new SpringApplication(VedioKycApplication.class);
    Properties properties = new Properties();
    properties.put("spring.data.mongodb.host", config.getDbHost());
    properties.put("spring.data.mongodb.port", config.getDbPort());
    properties.put("spring.data.mongodb.authentication-database", config.getAuthenticationDB());
    properties.put("spring.data.mongodb.username", config.getDbUsername());
    properties.put("spring.data.mongodb.password", config.getDbPassword());
    properties.put("spring.data.mongodb.database", config.getDatabase());
    properties.put("domainHostName", config.getDomainHostName());
    application.setDefaultProperties(properties);
    application.run(args);
  }
