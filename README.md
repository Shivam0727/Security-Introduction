
# Spring Security Project

## Overview
This repository contains a basic Spring Boot project with Spring Web and Security dependencies. The project demonstrates the implementation of Spring Security to handle authentication and authorization in a simple web application.

## Prerequisites

Before you begin, ensure you have the following installed :

### Java Development Kit (JDK)
### Apache Maven
### Your preferred IDE (e.g., IntelliJ, Eclipse)

## Getting Started
Clone this repository to your local machine :

### git-bash

    git clone https://github.com/your-username/spring-security-project.git

Open the project in your chosen IDE.

## Build the project using Maven:

    mvn clean install
    Run the application:


    mvn spring-boot:run
    The application will start on http://localhost:8080.

## Spring Security Configuration

The Spring Security configuration is defined in the SecurityConfig class located in the src/main/java/com/example/securityproject/config directory.

## Authentication

The project implements a basic in-memory user store for authentication. Users and their roles are configured in the SecurityConfig class:

- java

      @Override
      protected void configure(AuthenticationManagerBuilder auth) throws Exception {
            auth.inMemoryAuthentication()
            .withUser("user").password("{noop}password").roles("USER")
            .and()
            .withUser("admin").password("{noop}admin123").roles("USER", "ADMIN");
      }

In this example, two users are defined: "user" with the role "USER" and "admin" with roles "USER" and "ADMIN". Passwords are stored using {noop} to indicate plaintext passwords (for simplicity).

## Authorization

Authorization is configured using the HttpSecurity object in the same SecurityConfig class. For instance, restricting access to certain endpoints:

- java

      @Override
      protected void configure(HttpSecurity http) throws Exception {
           http.authorizeRequests()
          .antMatchers("/admin/**").hasRole("ADMIN")
          .antMatchers("/user/**").hasRole("USER")
          .anyRequest().authenticated()
          .and()
          .formLogin().permitAll()
          .and()
          .logout().permitAll();
      }

In this example, URLs starting with "/admin/" require the "ADMIN" role, and those starting with "/user/" require the "USER" role. Other URLs require authentication.

### Usage

    Access the application at http://localhost:8080.

## Use the following credentials for login:

    User: Username - user, Password - password (Role: USER)
    Admin: Username - admin, Password - admin123 (Roles: USER, ADMIN)

Explore the protected endpoints based on the configured roles.

## Contributing

Feel free to contribute by opening issues or creating pull requests. Your feedback is highly appreciated!

Happy coding! 🚀
