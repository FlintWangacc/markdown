# IREE runtime
## runtime backtrace
```bash
(lldb) bt
* thread #1, name = 'iree-run-module', stop reason = step in
  * frame #0: 0x00005555556416fe iree-run-module`iree_vm_bytecode_dispatch(stack=0x00007fffffff9c30, module=0x00005555556b3710, current_frame=0x00007fffffff9ca0, regs=iree_vm_registers_t @ 0x00007fffffff9900, call_results=(data = "", data_length = 16)) at dispatch.c:692:3
    frame #1: 0x000055555564166c iree-run-module`iree_vm_bytecode_dispatch_begin(stack=<unavailable>, module=<unavailable>, call=iree_vm_function_call_t @ 0x00007fffffff99e0, cconv_arguments=<unavailable>, cconv_results=<unavailable>) at dispatch.c:643:26
    frame #2: 0x0000555555640774 iree-run-module`iree_vm_bytecode_module_begin_call(self=0x00005555556b3710, stack=0x00007fffffff9c30, call=iree_vm_function_call_t @ 0x00007fffffff9a80) at module.c:850:10
    frame #3: 0x000055555568f69b iree-run-module`iree_vm_begin_invoke(state=<unavailable>, context=<unavailable>, function=iree_vm_function_t @ 0x00007fffffff9b70, flags=0, policy=<unavailable>, inputs=<unavailable>, host_allocator=iree_allocator_t @ 0x00007fffffff9bc8) at invocation.c:508:7
    frame #4: 0x000055555568f23b iree-run-module`iree_vm_invoke(context=0x0000555555f2acb0, function=iree_vm_function_t @ 0x000059c203538680, flags=0, policy=<unavailable>, inputs=0x0000555555f3b820, outputs=0x00005555558eb990, host_allocator=iree_allocator_t @ 0x00007fffffffbc68) at invocation.c:306:26
    frame #5: 0x00005555555c4860 iree-run-module`iree_tooling_run_function(context=0x0000555555f2acb0, function=iree_vm_function_t @ 0x00007fffffffbd20, device=0x000055555581b600, device_allocator=0x0000555555de2320, host_allocator=iree_allocator_t @ 0x00007fffffffbcb0, out_exit_code=0x00007fffffffbfac) at run_module.c:253:9 [inlined]
    frame #6: 0x00005555555c467b iree-run-module`iree_tooling_run_module_with_data(instance=<unavailable>, default_device_uri=(data = 0x0000000000000000, size = 0), module_contents=<unavailable>, host_allocator=iree_allocator_t @ 0x00007fffffffbf70, out_exit_code=0x00007fffffffbfac) at run_module.c:414:7
    frame #7: 0x00005555555c43c6 iree-run-module`iree_tooling_run_module_from_flags(instance=<unavailable>, host_allocator=iree_allocator_t @ 0x00007fffffffbf80, out_exit_code=<unavailable>) at run_module.c:388:10
    frame #8: 0x00005555555b8505 iree-run-module`main(argc=1, argv=0x00007fffffffc0e8) at iree-run-module-main.c:43:14
    frame #9: 0x00007ffff7a29d90 libc.so.6`__libc_start_call_main(main=(iree-run-module`main at iree-run-module-main.c:13), argc=6, argv=0x00007fffffffc0e8) at libc_start_call_main.h:58:16
    frame #10: 0x00007ffff7a29e40 libc.so.6`__libc_start_main_impl(main=(iree-run-module`main at iree-run-module-main.c:13), argc=6, argv=0x00007fffffffc0e8, init=<unavailable>, fini=<unavailable>, rtld_fini=<unavailable>, stack_end=0x00007fffffffc0d8) at libc-start.c:392:3
    frame #11: 0x00005555555b83d9 iree-run-module`_start + 41

```
## dispatch
iree_hal_command_buffer_vtable_t

## vm abi
**IREE** provides several VM ABIs. These ABIs are located in the file `runtime/src/iree/modules/hal/module.c` and are encapsulated using the macro `IREE_VM_ABI_EXPORT`.
| Function Name | Description |
|---------------|-------------|
| `iree_hal_module_devices_count`  | return the number of hal devices |

## hal.devices.get

<!--stackedit_data:
eyJoaXN0b3J5IjpbODk2NjI2NTk3XX0=
-->