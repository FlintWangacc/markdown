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

## iree_io_parameters_module_load
```bash
(lldb) bt
* thread #1, name = 'iree-run-module', stop reason = step over
  * frame #0: 0x00005555555d95c9 iree-run-module`iree_hal_hip_device_queue_read(base_device=0x000055555581b6a0, queue_affinity=1, wait_semaphore_list=iree_hal_semaphore_list_t @ 0x00007fffffff8ed0, signal_semaphore_list=iree_hal_semaphore_list_t @ 0x00007fffffff8ee8, source_file=0x0000555555850530, source_offset=67109248, target_buffer=0x00005555558506b0, target_offset=0, length=67108864, flags=0) at hip_device.c:2226:26
    frame #1: 0x00005555555c9b7a iree-run-module`iree_io_parameter_op_batch_enqueue_file_read(batch=0x00007fffffff9038, source_file=0x0000555555850530, source_file_offset=67109248, target_buffer=0x00005555558506b0, target_buffer_offset=0, length=67108864, flags=0) at parameter_index_provider.c:537:26
    frame #2: 0x00005555555c8ffd iree-run-module`iree_io_parameter_index_provider_load(base_provider=<unavailable>, device=0x000055555581b6a0, queue_affinity=<unavailable>, wait_semaphore_list=iree_hal_semaphore_list_t @ 0x00007fffffff91e0, signal_semaphore_list=iree_hal_semaphore_list_t @ 0x00007fffffff91f8, source_scope=<unavailable>, target_params=(usage = 527363, access = 0, type = 48, queue_affinity = 18446744073709551615, min_alignment = 0), count=3, enumerator=iree_io_parameter_enumerator_t @ 0x00007fffffff9230, emitter=iree_io_parameter_emitter_t @ 0x00007fffffff9240) at parameter_index_provider.c:798:22
    frame #3: 0x00005555555cba6c iree-run-module`iree_io_parameters_module_load(stack=<unavailable>, module=<unavailable>, state=0x0000555555ef8040, args=<unavailable>, rets=0x00007fffffff94e0) at module.c:324:14
    frame #4: 0x000055555569245b iree-run-module`iree_vm_native_module_issue_call(module=<unavailable>, stack=<unavailable>, callee_frame=<unavailable>, flags=<unavailable>, args_storage=<unavailable>, rets_storage=(data = "", data_length = 16)) at native_module.c:364:7
    frame #5: 0x00005555556922f9 iree-run-module`iree_vm_native_module_begin_call(self=0x00005555556b3d70, stack=0x00007fffffff98c0, call=iree_vm_function_call_t @ 0x00007fffffff9430) at native_module.c:420:10
    frame #6: 0x000055555564b474 iree-run-module`iree_vm_bytecode_issue_import_call(stack=0x00007fffffff98c0, call=iree_vm_function_call_t @ 0x00007fffffff94b0, cconv_results=<unavailable>, dst_reg_list=0x00005555556b6c6c, out_caller_frame=<unavailable>, out_caller_registers=<unavailable>) at dispatch.c:459:7
    frame #7: 0x000055555564ac4b iree-run-module`iree_vm_bytecode_call_import(stack=0x00007fffffff98c0, module_state=<unavailable>, import_ordinal=2147483668, caller_registers=iree_vm_registers_t @ 0x00005fcce2720e90, src_reg_list=0x00005555556b6c54, dst_reg_list=0x00005555556b6c6c, out_caller_frame=0x00007fffffff9688, out_caller_registers=0x00007fffffff9690) at dispatch.c:575:10
    frame #8: 0x0000555555645692 iree-run-module`iree_vm_bytecode_dispatch(stack=<unavailable>, module=<unavailable>, current_frame=0x00007fffffff9930, regs=iree_vm_registers_t @ 0x00007fffffff9690, call_results=(data = 0x0000000000000000, data_length = 0)) at dispatch.c:1692:5
    frame #9: 0x000055555564166c iree-run-module`iree_vm_bytecode_dispatch_begin(stack=<unavailable>, module=<unavailable>, call=iree_vm_function_call_t @ 0x00007fffffff9770, cconv_arguments=<unavailable>, cconv_results=<unavailable>) at dispatch.c:643:26
    frame #10: 0x0000555555640774 iree-run-module`iree_vm_bytecode_module_begin_call(self=0x00005555556b3710, stack=0x00007fffffff98c0, call=iree_vm_function_call_t @ 0x00007fffffff9810) at module.c:850:10
    frame #11: 0x000055555568e834 iree-run-module`iree_vm_context_run_function(context=<unavailable>, stack=0x00007fffffff98c0, module=0x00005555556b3710, function_name=<unavailable>) at context.c:91:12
    frame #12: 0x000055555568e2b1 iree-run-module`iree_vm_context_register_modules(context=0x0000555555e9b1b0, module_count=3, modules=0x00007fffffffb9a0) at context.c:596:14
    frame #13: 0x000055555568dfb8 iree-run-module`iree_vm_context_create_with_modules(instance=0x00005555556b32b0, flags=0, module_count=3, modules=0x00007fffffffb9a0, allocator=iree_allocator_t @ 0x00005fcce26e5b70, out_context=0x00007fffffffb978) at context.c:340:7
    frame #14: 0x00005555555bd1d6 iree-run-module`iree_tooling_create_context_from_flags(instance=0x00005555556b32b0, user_module_count=1, user_modules=<unavailable>, default_device_uri=(data = 0x0000000000000000, size = 0), host_allocator=iree_allocator_t @ 0x00007fffffffbbe0, out_context=0x00007fffffffbc70, out_device=0x00007fffffffbc60, out_device_allocator=0x00007fffffffbc30) at context_util.c:658:26
    frame #15: 0x00005555555c45aa iree-run-module`iree_tooling_create_run_context(instance=0x00005555556b32b0, default_device_uri=<unavailable>, module_contents=<unavailable>, host_allocator=iree_allocator_t @ 0x00005fcce26d52b0, out_context=<unavailable>, out_function=<unavailable>, out_device=<unavailable>, out_device_allocator=<unavailable>) at run_module.c:151:9 [inlined]
    frame #16: 0x00005555555c440a iree-run-module`iree_tooling_run_module_with_data(instance=0x00005555556b32b0, default_device_uri=(data = 0x0000000000000000, size = 0), module_contents=<unavailable>, host_allocator=iree_allocator_t @ 0x00007fffffffbef0, out_exit_code=0x00007fffffffbf2c) at run_module.c:405:3
    frame #17: 0x00005555555c43c6 iree-run-module`iree_tooling_run_module_from_flags(instance=<unavailable>, host_allocator=iree_allocator_t @ 0x00007fffffffbf00, out_exit_code=<unavailable>) at run_module.c:388:10
    frame #18: 0x00005555555b8505 iree-run-module`main(argc=1, argv=0x00007fffffffc068) at iree-run-module-main.c:43:14
    frame #19: 0x00007ffff7a29d90 libc.so.6`__libc_start_call_main(main=(iree-run-module`main at iree-run-module-main.c:13), argc=6, argv=0x00007fffffffc068) at libc_start_call_main.h:58:16
    frame #20: 0x00007ffff7a29e40 libc.so.6`__libc_start_main_impl(main=(iree-run-module`main at iree-run-module-main.c:13), argc=6, argv=0x00007fffffffc068, init=<unavailable>, fini=<unavailable>, rtld_fini=<unavailable>, stack_end=0x00007fffffffc058) at libc-start.c:392:3
    frame #21: 0x00005555555b83d9 iree-run-module`_start + 41

```
iree_hal_hip_device_queue_alloca

```bash
(lldb) bt
* thread #6, name = 'iree-run-module', stop reason = step over
  * frame #0: 0x00005555555da323 iree-run-module`iree_hal_hip_device_perform_buffer_operation_now(user_data=0x0000555555f0e180, status=0x0000000000000000) at hip_device.c:1482:7
    frame #1: 0x00005555555dee69 iree-run-module`iree_hal_hip_dispatch_thread_main(param=0x0000555555fa4750) at dispatch_thread.c:66:16
    frame #2: 0x0000555555639359 iree-run-module`iree_thread_start_routine(param=0x0000555555a27af0) at threading_pthreads.c:119:29
    frame #3: 0x00007ffff7a94ac3 libc.so.6`start_thread(arg=<unavailable>) at pthread_create.c:442:8
    frame #4: 0x00007ffff7b268c0 libc.so.6`__clone3 at clone3.S:81

```
iree_vm_bytecode_dispatch
iree_io_parameters_module_load

iree_vm_abi_rIrrrIiirrr_t

```bash
(lldb) bt
* thread #1, name = 'iree-run-module', stop reason = step over
  * frame #0: 0x0000555555609096 iree-run-module`iree_hal_hip_device_queue_alloca(base_device=0x00005555558f1680, queue_affinity=1, wait_semaphore_list=iree_hal_semaphore_list_t @ 0x00007fffffff4d70, signal_semaphore_list=iree_hal_semaphore_list_t @ 0x00007fffffff4d88, pool=0, params=(usage = 527363, access = 0, type = 48, queue_affinity = 18446744073709551615, min_alignment = 0), allocation_size=67108864, flags=0, out_buffer=0x00007fffffff4ff0) at hip_device.c:1646:11
    frame #1: 0x00005555555da7fc iree-run-module`iree_hal_device_queue_alloca(device=0x00005555558f1680, queue_affinity=18446744073709551615, wait_semaphore_list=iree_hal_semaphore_list_t @ 0x00007fffffff4e40, signal_semaphore_list=iree_hal_semaphore_list_t @ 0x00007fffffff4e58, pool=0, params=(usage = 527363, access = 0, type = 48, queue_affinity = 18446744073709551615, min_alignment = 0), allocation_size=67108864, flags=0, out_buffer=0x00007fffffff4ff0) at device.c:97:26
    frame #2: 0x00005555555ed5a3 iree-run-module`iree_io_parameter_op_batch_enqueue_alloca(batch=0x00007fffffff5038, pool=0, params=(usage = 527363, access = 0, type = 48, queue_affinity = 18446744073709551615, min_alignment = 0), allocation_size=67108864, out_buffer=0x00007fffffff4ff0) at parameter_index_provider.c:473:3
    frame #3: 0x00005555555ec6ac iree-run-module`iree_io_parameter_index_provider_load(base_provider=0x0000555555789cd0, device=0x00005555558f1680, queue_affinity=18446744073709551615, wait_semaphore_list=iree_hal_semaphore_list_t @ 0x00007fffffff51b0, signal_semaphore_list=iree_hal_semaphore_list_t @ 0x00007fffffff51c8, source_scope=(data = "global", size = 6), target_params=(usage = 527363, access = 0, type = 48, queue_affinity = 18446744073709551615, min_alignment = 0), count=3, enumerator=iree_io_parameter_enumerator_t @ 0x00007fffffff5200, emitter=iree_io_parameter_emitter_t @ 0x00007fffffff5210) at parameter_index_provider.c:781:16
    frame #4: 0x00005555555f28bb iree-run-module`iree_io_parameter_provider_load(provider=0x0000555555789cd0, device=0x00005555558f1680, queue_affinity=18446744073709551615, wait_semaphore_list=iree_hal_semaphore_list_t @ 0x00007fffffff52c0, signal_semaphore_list=iree_hal_semaphore_list_t @ 0x00007fffffff52d8, source_scope=(data = "global", size = 6), target_params=(usage = 527363, access = 0, type = 48, queue_affinity = 18446744073709551615, min_alignment = 0), count=3, enumerator=iree_io_parameter_enumerator_t @ 0x00007fffffff5310, emitter=iree_io_parameter_emitter_t @ 0x00007fffffff5320) at parameter_provider.c:66:26
    frame #5: 0x00005555555f1912 iree-run-module`iree_io_parameters_module_load(stack=0x00007fffffff96a0, module=0x0000555555789d70, state=0x0000555555f92a70, args=0x00007fffffff5820, rets=0x00007fffffff5810) at module.c:324:14
    frame #6: 0x0000555555766a20 iree-run-module`iree_vm_shim_rIrrrIiirrr_r(stack=0x00007fffffff96a0, flags=1, args_storage=(data = "\x80\U00000016\x8fUUU", data_length = 136), rets_storage=(data = "", data_length = 16), target_fn=(iree-run-module`iree_io_parameters_module_load at module.c:272), module=0x0000555555789d70, module_state=0x0000555555f92a70) at shims.c:80:1
    frame #7: 0x0000555555760c44 iree-run-module`iree_vm_native_module_issue_call(module=0x0000555555789d70, stack=0x00007fffffff96a0, callee_frame=0x00007fffffff9870, flags=1, args_storage=(data = "\x80\U00000016\x8fUUU", data_length = 136), rets_storage=(data = "", data_length = 16)) at native_module.c:364:7
    frame #8: 0x0000555555760820 iree-run-module`iree_vm_native_module_begin_call(self=0x0000555555789d70, stack=0x00007fffffff96a0, call=iree_vm_function_call_t @ 0x00007fffffff56e0) at native_module.c:420:10
    frame #9: 0x00005555556c8f30 iree-run-module`iree_vm_bytecode_issue_import_call(stack=0x00007fffffff96a0, call=iree_vm_function_call_t @ 0x00007fffffff57e0, cconv_results=(data = "r", size = 1), dst_reg_list=0x000055555578cc6c, out_caller_frame=0x00007fffffff9378, out_caller_registers=0x00007fffffff9390) at dispatch.c:459:7
    frame #10: 0x00005555556c6a74 iree-run-module`iree_vm_bytecode_call_import(stack=0x00007fffffff96a0, module_state=0x00005555560bf6a0, import_ordinal=2147483668, caller_registers=iree_vm_registers_t @ 0x00007fffffff5928, src_reg_list=0x000055555578cc54, dst_reg_list=0x000055555578cc6c, out_caller_frame=0x00007fffffff9378, out_caller_registers=0x00007fffffff9390) at dispatch.c:575:10
    frame #11: 0x00005555556ba926 iree-run-module`iree_vm_bytecode_dispatch(stack=0x00007fffffff96a0, module=0x0000555555789710, current_frame=0x00007fffffff9710, regs=iree_vm_registers_t @ 0x00007fffffff9390, call_results=(data = 0x0000000000000000, data_length = 0)) at dispatch.c:1708:10
    frame #12: 0x00005555556adc30 iree-run-module`iree_vm_bytecode_dispatch_begin(stack=0x00007fffffff96a0, module=0x0000555555789710, call=iree_vm_function_call_t @ 0x00007fffffff9470, cconv_arguments=(data = 0x0000000000000000, size = 0), cconv_results=(data = 0x0000000000000000, size = 0)) at dispatch.c:643:26
    frame #13: 0x00005555556a9215 iree-run-module`iree_vm_bytecode_module_begin_call(self=0x0000555555789710, stack=0x00007fffffff96a0, call=iree_vm_function_call_t @ 0x00007fffffff9540) at module.c:850:10
    frame #14: 0x0000555555756f51 iree-run-module`iree_vm_context_run_function(context=0x00005555557cdc30, stack=0x00007fffffff96a0, module=0x0000555555789710, function_name=(data = "__init", size = 6)) at context.c:91:12
    frame #15: 0x0000555555756151 iree-run-module`iree_vm_context_register_modules(context=0x00005555557cdc30, module_count=3, modules=0x00007fffffffb828) at context.c:596:14
    frame #16: 0x0000555555755aa9 iree-run-module`iree_vm_context_create_with_modules(instance=0x00005555557892b0, flags=0, module_count=3, modules=0x00007fffffffb828, allocator=iree_allocator_t @ 0x00007fffffffb788, out_context=0x00007fffffffb7f0) at context.c:340:7
    frame #17: 0x00005555555d6a41 iree-run-module`iree_tooling_create_context_from_flags(instance=0x00005555557892b0, user_module_count=1, user_modules=0x00007fffffffbb60, default_device_uri=(data = 0x0000000000000000, size = 0), host_allocator=iree_allocator_t @ 0x00007fffffffba80, out_context=0x00007fffffffbaf8, out_device=0x00007fffffffbaf0, out_device_allocator=0x00007fffffffbae8) at context_util.c:658:26
    frame #18: 0x00005555555e4d62 iree-run-module`iree_tooling_create_run_context(instance=0x00005555557892b0, default_device_uri=(data = 0x0000000000000000, size = 0), module_contents=(data = 0x0000000000000000, data_length = 0), host_allocator=iree_allocator_t @ 0x00007fffffffbdb0, out_context=0x00007fffffffbe38, out_function=0x00007fffffffbe28, out_device=0x00007fffffffbe20, out_device_allocator=0x00007fffffffbe18) at run_module.c:151:9
    frame #19: 0x00005555555e48e8 iree-run-module`iree_tooling_run_module_with_data(instance=0x00005555557892b0, default_device_uri=(data = 0x0000000000000000, size = 0), module_contents=(data = 0x0000000000000000, data_length = 0), host_allocator=iree_allocator_t @ 0x00007fffffffbea0, out_exit_code=0x00007fffffffbf14) at run_module.c:405:3
    frame #20: 0x00005555555e482b iree-run-module`iree_tooling_run_module_from_flags(instance=0x00005555557892b0, host_allocator=iree_allocator_t @ 0x00007fffffffbef0, out_exit_code=0x00007fffffffbf14) at run_module.c:388:10
    frame #21: 0x00005555555cf851 iree-run-module`main(argc=1, argv=0x00007fffffffc068) at iree-run-module-main.c:43:14
    frame #22: 0x00007ffff7a29d90 libc.so.6`__libc_start_call_main(main=(iree-run-module`main at iree-run-module-main.c:13), argc=6, argv=0x00007fffffffc068) at libc_start_call_main.h:58:16
    frame #23: 0x00007ffff7a29e40 libc.so.6`__libc_start_main_impl(main=(iree-run-module`main at iree-run-module-main.c:13), argc=6, argv=0x00007fffffffc068, init=<unavailable>, fini=<unavailable>, rtld_fini=<unavailable>, stack_end=0x00007fffffffc058) at libc-start.c:392:3
    frame #24: 0x00005555555cf709 iree-run-module`_start + 41
```
iree_io_parameter_op_batch_enqueue_alloca

device.c:243
```bash
(lldb) bt
* thread #7, name = 'iree-run-module', stop reason = step over
  * frame #0: 0x00005555556211b9 iree-run-module`iree_hal_hip_stream_command_buffer_begin(base_command_buffer=0x00007ffe8c003720) at stream_command_buffer.c:187:3
    frame #1: 0x00005555555df748 iree-run-module`iree_hal_command_buffer_begin(command_buffer=0x00007ffe8c003720) at command_buffer.c:274:7
    frame #2: 0x0000555555619154 iree-run-module`iree_hal_hip_multi_queue_command_buffer_begin(base_command_buffer=0x00007ffe8c00b810) at hip_multi_queue_command_buffer.c:158:3
    frame #3: 0x00005555555df748 iree-run-module`iree_hal_command_buffer_begin(command_buffer=0x00007ffe8c00b810) at command_buffer.c:274:7
    frame #4: 0x000055555560c336 iree-run-module`iree_hal_hip_device_perform_queue_read_now(user_data=0x0000555555fe6450, status=0x0000000000000000) at hip_device.c:2076:16
    frame #5: 0x000055555561224d iree-run-module`iree_hal_hip_dispatch_thread_main(param=0x0000555555ed9600) at dispatch_thread.c:66:16
    frame #6: 0x000055555569e205 iree-run-module`iree_thread_start_routine(param=0x0000555555f47f20) at threading_pthreads.c:119:29
    frame #7: 0x00007ffff7a94ac3 libc.so.6`start_thread(arg=<unavailable>) at pthread_create.c:442:8
    frame #8: 0x00007ffff7b268c0 libc.so.6`__clone3 at clone3.S:81
```

parameter_index_provider.c:690
`iree_hal_hip_device_complete_buffer_operation`
`./runtime/src/iree/io/parameter_index_provider.c:786`
## IREE_HAL objects on hip platform
| hal object | hip object | location |
|---------------|-------------|-------------|
| `iree_hal_semaphore_t` | `iree_hal_hip_semaphore_t`| `hal/drivers/hip/event_semaphore.c:124` |
|`iree_hal_buffer_t`| `iree_hal_hip_buffer_t`|`runtime/src/iree/hal/drivers/hip/hip_buffer.c:27`|

`iree_hal_hip_device_make_buffer_callback_data` which initialize the dispatch item for dispatch thread.

`iree_hal_hip_native_executable_create` debugging
`iree_hal_command_buffer_create` debugging
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTkwMTc4OTY4NywtNjIxNDgzODBdfQ==
-->