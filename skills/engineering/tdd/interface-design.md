# Interface Design for Testability

Good interfaces make testing natural:

1. **Accept dependencies, don't create them**

   ```typescript
   // Testable
   function processOrder(order, paymentGateway) {}

   // Hard to test
   function processOrder(order) {
     const gateway = new StripeGateway();
   }
   ```

2. **Return results, don't produce side effects**

   ```typescript
   // Testable
   function calculateDiscount(cart): Discount {}

   // Hard to test
   function applyDiscount(cart): void {
     cart.total -= discount;
   }
   ```

3. **Small surface area**
   - Fewer methods = fewer tests needed
   - Fewer params = simpler test setup

4. **Expose outcomes, not internals**

   ```typescript
   // Testable
   const receipt = await checkout(cart, paymentMethod);
   expect(receipt.status).toBe("confirmed");

   // Brittle
   expect(paymentGateway.charge).toHaveBeenCalledTimes(1);
   ```

5. **Make failure modes explicit**
   - Return or throw domain-specific errors callers can assert on
   - Avoid forcing tests to inspect logs, database rows, or private fields to know what happened
