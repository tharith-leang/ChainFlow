# Security Specification for ChainFlow

## Data Invariants
1. **User Role Integrity**: A user cannot change their own `role` or `isAdmin` status.
2. **Product Ownership**: Only the `supplier` who created a product (or an `admin`) can edit or delete it.
3. **Order Privacy**: Customers can only see their own orders. Suppliers can only see orders for their products. Admins can see everything.
4. **Chat Privacy**: Only users listed in the `participants` array of a conversation can read or write messages in that conversation.
5. **Inventory Accuracy**: `status` must be `out-of-stock` if `quantity` is 0.

## The Dirty Dozen Payloads (Rejection Targets)

1. **Self-Promotion**: A customer attempts to update their `role` to `admin`.
2. **Product Hijack**: Supplier A attempts to update a product owned by Supplier B.
3. **Ghost Product**: Creating a product with a missing `supplierId` or `price`.
4. **Negative Stock**: Updating product `quantity` to -5.
5. **Shadow Message**: Sending a message to a conversation where the user is NOT a participant.
6. **Impersonation**: Updating a message `senderId` to another user's UID.
7. **Order Snooping**: Customer B attempts to 'get' an order belonging to Customer A.
8. **Malicious ID**: Creating a product with an ID containing malicious characters like `../../../etc/passwd`.
9. **Spam Attack**: Attempting to create a message with a text size of 1MB.
10. **Delivery Spoofing**: A customer attempts to update their order status to `delivered`.
11. **Orphaned Message**: Creating a message in a conversation that doesn't exist.
12. **Timestamp Fraud**: Setting `createdAt` to a future date instead of `request.time`.

## Test Runner (Draft)
Verification will be handled via manual testing and rules simulation during development.
