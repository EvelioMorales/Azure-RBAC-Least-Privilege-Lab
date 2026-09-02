# Recommended follow-up improvements

## Capture a clean RBAC denial

The current write-test screenshot shows that `Microsoft.Compute` was not registered and that the Reader identity could not register it. To isolate the RBAC behavior:

1. Sign in with an authorized administrator account.
2. Register the `Microsoft.Compute` resource provider.
3. Return to the separate `cloudreader` session.
4. Attempt a harmless write operation within `rg-security-lab`.
5. Capture the `AuthorizationFailed` result and related Azure Activity Log event.
6. Do not submit or deploy a billable resource.

## Add monitoring evidence

Capture a filtered Activity Log event showing the restricted identity, failed operation, timestamp, scope, and status. Redact the caller UPN, subscription ID, correlation ID, and any public IP address before publication.

## Add infrastructure as code

A future version could create the resource group and role assignment with Terraform. The test user should remain an input rather than placing credentials or secrets in code. Use remote state protection, pin provider versions, run `terraform plan`, and destroy the lab after validation.

