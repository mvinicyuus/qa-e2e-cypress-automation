# qa-e2e-cypress-automation
## Cypress Test  Arquivo de teste E2E utilizando Cypress.  

### Cenário 
- Login 
- Busca de produto 
- Adição ao carrinho 
- Validação do carrinho

### Script de teste

describe('Fluxo de compra - Automation Exercise', () => {

  it('Login + buscar produto + adicionar ao carrinho + validar checkout', () => {

    // 🔐 Acessar página de login
    cy.visit('https://www.automationexercise.com/login')

    // Login
    cy.get('[data-qa="login-email"]').type('teste2024@teste.com.br')
    cy.get('[data-qa="login-password"]').type('teste')
    cy.get('[data-qa="login-button"]').click()

    // ✅ Valida login com sucesso
    cy.contains('Logged in as').should('be.visible')

    // 📦 Acessar página de produtos
    cy.contains('a', 'Products').click()
    cy.url().should('include', '/products')

    // 🛒 2 - Incluir produto no carrinho (garantindo apenas 1 clique)
    cy.get('[data-product-id="2"]')
      .should('have.length.at.least', 1)
      .then(($el) => {
        cy.wrap($el[0]).click()
      })

    // Modal → ir para o carrinho
    cy.contains('View Cart').click()

    // 💳 3 - Validar produtos no carrinho
    cy.url().should('include', '/view_cart')

    cy.get('.cart_description')
      .should('be.visible')

    // Validar que existe apenas 1 produto no carrinho
    cy.get('.cart_product')
      .should('have.length', 1)

  })

})
