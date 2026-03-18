# qa-e2e-cypress-automation
## Cypress Test  Arquivo de teste E2E utilizando Cypress.  

### Cenário 
- Login 
- Busca de produto 
- Adição ao carrinho 
- Validação do carrinho

### 🧪 Test Script

```javascript
describe('Purchase Flow - Automation Exercise', () => {

  it('Login, add product to cart and validate checkout', () => {

    // 🔐 Login
    cy.visit('https://www.automationexercise.com/login')

    cy.get('[data-qa="login-email"]').type('teste2024@teste.com.br')
    cy.get('[data-qa="login-password"]').type('teste')
    cy.get('[data-qa="login-button"]').click()

    // ✅ Validate successful login
    cy.contains('Logged in as').should('be.visible')

    // 📦 Navigate to Products page
    cy.contains('a', 'Products').click()
    cy.url().should('include', '/products')

    // 🛒 Add a single product to cart
    cy.get('[data-product-id="2"]')
      .first()
      .click()

    // 🧾 Go to cart
    cy.contains('View Cart').click()

    // 💳 Validate cart page
    cy.url().should('include', '/view_cart')

    cy.get('.cart_description')
      .should('be.visible')

    // ✅ Ensure only one product is in the cart
    cy.get('.cart_product')
      .should('have.length', 1)

  })

})
