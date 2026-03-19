# qa-e2e-cypress-automation
## Cypress Test  Arquivo de teste E2E utilizando Cypress.  

### Cenário BDD
Feature: Purchase flow

  Scenario: Login and add product to cart

    Given I access the login page
    When I login with valid credentials
    And I navigate to products page
    And I add a product to the cart
    And I go to the cart
    Then I should see 1 product in the cart

### 🧪 Test Script

```javascript
const { Given, When, Then } = require("@badeball/cypress-cucumber-preprocessor");

// 🔐 Acessar página de login
Given("I access the login page", () => {
  cy.visit('https://www.automationexercise.com/login')
})

// 🔑 Realizar login
When("I login with valid credentials", () => {
  cy.get('[data-qa="login-email"]').type('teste2024@teste.com.br')
  cy.get('[data-qa="login-password"]').type('teste')
  cy.get('[data-qa="login-button"]').click()

  cy.contains('Logged in as').should('be.visible')
})

// 📦 Navegar para produtos
When("I navigate to products page", () => {
  cy.contains('a', 'Products').click()
  cy.url().should('include', '/products')
})

// 🛒 Adicionar produto ao carrinho
When("I add a product to the cart", () => {
  cy.get('[data-product-id="2"]').first().click()
})

// 🧾 Ir para o carrinho
When("I go to the cart", () => {
  cy.contains('View Cart').click()
})

// ✅ Validar carrinho
Then("I should see 1 product in the cart", () => {
  cy.url().should('include', '/view_cart')

  cy.get('.cart_description')
    .should('be.visible')

  cy.get('.cart_product')
    .should('have.length', 1)
})
