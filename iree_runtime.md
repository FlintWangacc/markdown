# IREE runtime
## runtime backtrace
```bash
(lldb) bt
* thread #1, name = 'iree-run-module', stop reason = step over
  * frame #0: 0x0000555555645489 iree-run-module`iree_vm_bytecode_dispatch(stack=0x00007fffffff9940, module=0x00005555556b3710, current_frame=0x00007fffffff99b0, regs=iree_vm_registers_t @ 0x00007fffffff9710, call_results=(data = 0x0000000000000000, data_length = 0)) at dispatch.c:1314:5
    frame #1: 0x000055555564166c iree-run-module`iree_vm_bytecode_dispatch_begin(stack=<unavailable>, module=<unavailable>, call=iree_vm_function_call_t @ 0x00007fffffff97f0, cconv_arguments=<unavailable>, cconv_results=<unavailable>) at dispatch.c:643:26
    frame #2: 0x0000555555640774 iree-run-module`iree_vm_bytecode_module_begin_call(self=0x00005555556b3710, stack=0x00007fffffff9940, call=iree_vm_function_call_t @ 0x00007fffffff9890) at module.c:850:10
    frame #3: 0x000055555568e834 iree-run-module`iree_vm_context_run_function(context=<unavailable>, stack=0x00007fffffff9940, module=0x00005555556b3710, function_name=<unavailable>) at context.c:91:12
    frame #4: 0x000055555568e2b1 iree-run-module`iree_vm_context_register_modules(context=0x0000555555f2acb0, module_count=3, modules=0x00007fffffffba20) at context.c:596:14
    frame #5: 0x000055555568dfb8 iree-run-module`iree_vm_context_create_with_modules(instance=0x00005555556b32b0, flags=0, module_count=3, modules=0x00007fffffffba20, allocator=iree_allocator_t @ 0x00006298203c28d0, out_context=0x00007fffffffb9f8) at context.c:340:7
    frame #6: 0x00005555555bd1d6 iree-run-module`iree_tooling_create_context_from_flags(instance=0x00005555556b32b0, user_module_count=1, user_modules=<unavailable>, default_device_uri=(data = 0x0000000000000000, size = 0), host_allocator=iree_allocator_t @ 0x00007fffffffbc60, out_context=0x00007fffffffbcf0, out_device=0x00007fffffffbce0, out_device_allocator=0x00007fffffffbcb0) at context_util.c:658:26
    frame #7: 0x00005555555c45aa iree-run-module`iree_tooling_create_run_context(instance=0x00005555556b32b0, default_device_uri=<unavailable>, module_contents=<unavailable>, host_allocator=iree_allocator_t @ 0x000062981fe2b920, out_context=<unavailable>, out_function=<unavailable>, out_device=<unavailable>, out_device_allocator=<unavailable>) at run_module.c:151:9 [inlined]
    frame #8: 0x00005555555c440a iree-run-module`iree_tooling_run_module_with_data(instance=0x00005555556b32b0, default_device_uri=(data = 0x0000000000000000, size = 0), module_contents=<unavailable>, host_allocator=iree_allocator_t @ 0x00007fffffffbf70, out_exit_code=0x00007fffffffbfac) at run_module.c:405:3
    frame #9: 0x00005555555c43c6 iree-run-module`iree_tooling_run_module_from_flags(instance=<unavailable>, host_allocator=iree_allocator_t @ 0x00007fffffffbf80, out_exit_code=<unavailable>) at run_module.c:388:10
    frame #10: 0x00005555555b8505 iree-run-module`main(argc=1, argv=0x00007fffffffc0e8) at iree-run-module-main.c:43:14
    frame #11: 0x00007ffff7a29d90 libc.so.6`__libc_start_call_main(main=(iree-run-module`main at iree-run-module-main.c:13), argc=6, argv=0x00007fffffffc0e8) at libc_start_call_main.h:58:16
    frame #12: 0x00007ffff7a29e40 libc.so.6`__libc_start_main_impl(main=(iree-run-module`main at iree-run-module-main.c:13), argc=6, argv=0x00007fffffffc0e8, init=<unavailable>, fini=<unavailable>, rtld_fini=<unavailable>, stack_end=0x00007fffffffc0d8) at libc-start.c:392:3
    frame #13: 0x00005555555b83d9 iree-run-module`_start + 41
```
## dispatch
iree_hal_command_buffer_vtable_t

## vm abi
**IREE** provides several VM ABIs. These ABIs are located in the file `runtime/src/iree/modules/hal/module.c` and are encapsulated using the macro `IREE_VM_ABI_EXPORT`.
| Function Name |Description| vm bytecode |
|---------------|-------------|-------------|
| `iree_hal_module_devices_count`  | return the number of hal devices |  NA  |
| `iree_hal_module_devices_get` |  NA | `hal.devices.get`|

## note
iree virtual machine will call import functions for management tasks.

## iree_hal_executable_cache_prepare_executable
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjEyMTk3MDg4Ml19
-->