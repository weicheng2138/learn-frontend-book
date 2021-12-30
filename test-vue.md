---
description: Test with vue composition api.
---

# Test Vue

## Unit Test

* <mark style="color:blue;">shallowMount</mark> will mount only the parent elements but not child element, which help us to direct test the surface of parent behavior without rendering children elements. `<vuecomp-stub>`

```
// Use function to declare a higher order variable for the test
const factory = (props) => {
    return mount(DraggableDemo, {
        propsData: {
            ...props,
        },
    })
}
```

### To `call` or to `mount`? <a href="#to-call-or-to-mount" id="to-call-or-to-mount"></a>

###
