---
# generated by https://github.com/hashicorp/terraform-plugin-docs
page_title: "commercetools_state_transitions Resource - terraform-provider-commercetools"
subcategory: ""
description: |-
  Transitions are a way to describe possible transformations of the current state to other states of the same type (for example: Initial -> Shipped). When performing a transitionState update action and transitions is set, the currently referenced state must have a transition to the new state.
  If transitions is an empty list, it means the current state is a final state and no further transitions are allowed.
  If transitions is not set, the validation is turned off. When performing a transitionState update action, any other state of the same type can be transitioned to.
  Note: Only one resource can be created for each state
---

# commercetools_state_transitions (Resource)

Transitions are a way to describe possible transformations of the current state to other states of the same type (for example: Initial -> Shipped). When performing a transitionState update action and transitions is set, the currently referenced state must have a transition to the new state.
If transitions is an empty list, it means the current state is a final state and no further transitions are allowed.
If transitions is not set, the validation is turned off. When performing a transitionState update action, any other state of the same type can be transitioned to.

Note: Only one resource can be created for each state

## Example Usage

```terraform
resource "commercetools_state" "product_for_sale" {
  key  = "product-for-sale"
  type = "ProductState"
  name = {
    en = "For Sale"
  }
  description = {
    en = "Regularly stocked product."
  }
  initial = true
}

resource "commercetools_state" "product_clearance" {
  key  = "product-clearance"
  type = "ProductState"
  name = {
    en = "On Clearance"
  }
  description = {
    en = "The product line will not be ordered again."
  }
}


// Only allow transition from sale to clearance
resource "commercetools_state_transitions" "transition_1" {
  from = commercetools_state.product_for_sale.id
  to = [
    commercetools_state.product_clearance.id,
  ]
}

// Disable transitions from product clearance to other
resource "commercetools_state_transitions" "transition_2" {
  from = commercetools_state.product_clearance.id
  to   = []
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `from` (String) ID of the state to transition from
- `to` (Set of String) Transitions are a way to describe possible transformations of the current state to other states of the same type (for example: Initial -> Shipped). When performing a transitionState update action and transitions is set, the currently referenced state must have a transition to the new state.
If transitions is an empty list, it means the current state is a final state and no further transitions are allowed.
If transitions is not set, the validation is turned off. When performing a transitionState update action, any other state of the same type can be transitioned to

### Read-Only

- `id` (String) The ID of this resource.

