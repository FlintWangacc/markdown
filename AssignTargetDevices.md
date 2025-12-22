# AssignTargetDevicesPass
## Pass description
```mlir
     Assigns target HAL devices to the module based on the given list of target
      specifications.

      Targets can be specified in several ways depending on whether there are
      multiple devices, named devices, or devices imported from external files.
      Human-friendly device aliases can be used as shorthand for
      `IREE::HAL::TargetDevice` implementations providing their own configuration.
      The aliases are identical to those used by `#hal.device.alias<>`.

      If multiple targets are specified they will be available as multiple
      distinct devices. A single device may select from one or more targets such
      that the first enumerated that matches at runtime will be selected. For
      example a `gpu` device may select between CUDA, HIP, or Vulkan at runtime
      based on what kind of device the user has and what HAL implementations were
      compiled into the runtime.

      Examples using the canonical flag:
      ```mlir
      // Two devices, one the local host device and the other a Vulkan device:
      --iree-hal-target-device=local
      --iree-hal-target-device=vulkan

      // One device selecting between Vulkan if available and otherwise use the
      // local host device:
      --iree-hal-target-device=vulkan,local

      // Two CUDA devices selected by runtime ordinal; at runtime two --device=
      // flags are required to configure both devices:
      --iree-hal-target-device=cuda[0]
      --iree-hal-target-device=cuda[1]

      // A fully-defined target specification:
      --iree-hal-target-device=#hal.device.target<"cuda", {...}, [#hal.executable.target<...>]>

      // Named device for defining a reference by #hal.device.promise<@some_name>:
      --iree-hal-target-device=some_name=vulkan
      ```


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzNDI5MTEzMywxMTg2NTIyOTYxXX0=
-->