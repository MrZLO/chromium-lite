PROJECT(chromium-base C CXX)

CMAKE_MINIMUM_REQUIRED(VERSION 2.8.8)
SET(CMAKE_BUILD_TYPE Debug)
SET(CMAKE_POSITION_INDEPENDENT_CODE ON)

SET(PROJECT_NAME "Chromium - Base")

# CMake modules
INCLUDE(FindThreads)
INCLUDE(FindPkgConfig)
INCLUDE(GNUInstallDirs)

# Mandatory dependencies
FIND_PACKAGE(Threads)
PKG_CHECK_MODULES(libevent REQUIRED libevent)
PKG_CHECK_MODULES(icui18n REQUIRED icu-i18n)

# Common definitions
ADD_DEFINITIONS(-DOS_POSIX=1 -DCOMPONENT_BUILD=1 -DBASE_IMPLEMENTATION=1)

IF(CMAKE_COMPILER_IS_GNUCXX)
    ADD_DEFINITIONS(-std=c++11)
ENDIF()


# SOURCES FILE LIST, PER SECTION

# switches
ADD_LIBRARY(switches OBJECT base_switches.cc)

# command_line
ADD_LIBRARY(command_line OBJECT command_line.cc)

# strings
ADD_LIBRARY(strings OBJECT third_party/icu/icu_utf.cc third_party/dmg_fp/g_fmt.cc third_party/dmg_fp/dtoa.cc strings/utf_string_conversion_utils.cc strings/utf_string_conversions.cc strings/utf_offset_string_conversions.cc strings/string16.cc strings/string_piece.cc strings/string_util.cc strings/string_util_constants.cc strings/string_split.cc strings/stringprintf.cc strings/sys_string_conversions_posix.cc strings/string_number_conversions.cc strings/pattern.cc json/string_escape.cc json/json_writer.cc json/json_reader.cc json/json_parser.cc json/json_string_value_serializer.cc)

# logging
ADD_LIBRARY(logging OBJECT logging.cc trace_event/trace_log.cc trace_event/trace_log_constants.cc trace_event/trace_config.cc trace_event/trace_buffer.cc trace_event/trace_event_impl.cc trace_event/malloc_dump_provider.cc trace_event/process_memory_totals_dump_provider.cc  trace_event/trace_event_synthetic_delay.cc trace_event/trace_event_memory_overhead.cc trace_event/memory_dump_manager.cc trace_event/memory_dump_request_args.cc trace_event/process_memory_dump.cc trace_event/memory_dump_session_state.cc trace_event/memory_allocator_dump.cc trace_event/process_memory_maps.cc trace_event/process_memory_totals.cc trace_event/heap_profiler_heap_dump_writer.cc trace_event/heap_profiler_stack_frame_deduplicator.cc trace_event/heap_profiler_type_name_deduplicator.cc trace_event/heap_profiler_allocation_context.cc trace_event/heap_profiler_allocation_context_tracker.cc trace_event/process_memory_maps_dump_provider.cc trace_event/memory_allocator_dump_guid.cc trace_event/trace_sampling_thread.cc trace_event/trace_event_argument.cc)

# i18n
ADD_LIBRARY(i18n OBJECT i18n/base_i18n_switches.cc i18n/bidi_line_iterator.cc i18n/break_iterator.cc i18n/build_utf8_validator_tables.cc i18n/case_conversion.cc i18n/char_iterator.cc i18n/file_util_icu.cc i18n/i18n_constants.cc i18n/icu_encoding_detection.cc i18n/icu_string_conversions.cc i18n/icu_util.cc i18n/number_formatting.cc i18n/rtl.cc i18n/streaming_utf8_validator.cc i18n/string_compare.cc i18n/string_search.cc i18n/timezone.cc i18n/utf8_validator_tables.cc)

# debug
ADD_LIBRARY(debug OBJECT debug/debugger.cc debug/debugger_posix.cc debug/stack_trace.cc debug/stack_trace_posix.cc debug/task_annotator.cc debug/alias.cc)

# lock
ADD_LIBRARY(lock OBJECT synchronization/lock.cc synchronization/lock_impl_posix.cc synchronization/waitable_event_posix.cc synchronization/waitable_event_watcher_posix.cc synchronization/condition_variable_posix.cc synchronization/cancellation_flag.cc)

# memory
ADD_LIBRARY(memory OBJECT memory/singleton.cc memory/aligned_memory.cc memory/ref_counted.cc memory/ref_counted_memory.cc memory/weak_ptr.cc allocator/allocator_extension.cc)

# message_loop
ADD_LIBRARY(messageloop OBJECT message_loop/message_loop.cc message_loop/message_loop_task_runner.cc message_loop/message_pump.cc message_loop/message_pump_default.cc message_loop/message_pump_libevent.cc message_loop/incoming_task_queue.cc run_loop.cc)

# version
ADD_LIBRARY(version OBJECT version.cc)

# vlog
ADD_LIBRARY(vlog OBJECT vlog.cc)

# pickle
ADD_LIBRARY(pickle OBJECT pickle.cc)

# base_paths
ADD_LIBRARY(paths OBJECT base_paths.cc base_paths_posix.cc)

# at_exit
ADD_LIBRARY(atexit OBJECT at_exit.cc)

# callback
ADD_LIBRARY(callback OBJECT callback_internal.cc)

# lazy_instance
ADD_LIBRARY(lazyinstance OBJECT lazy_instance.cc)

# posix
ADD_LIBRARY(posix OBJECT posix/file_descriptor_shuffle.cc posix/global_descriptors.cc posix/unix_domain_socket_linux.cc)

# sys_info
ADD_LIBRARY(sysinfo OBJECT sys_info.cc sys_info_posix.cc sys_info_linux.cc)

# threading
ADD_LIBRARY(threading OBJECT threading/thread.cc threading/simple_thread.cc threading/platform_thread_linux.cc threading/platform_thread_posix.cc threading/platform_thread_internal_posix.cc threading/thread_local_posix.cc threading/thread_local_storage.cc threading/thread_local_storage_posix.cc threading/thread_collision_warner.cc threading/thread_restrictions.cc threading/thread_id_name_manager.cc threading/thread_checker_impl.cc threading/worker_pool.cc threading/worker_pool_posix.cc threading/sequenced_worker_pool.cc threading/non_thread_safe_impl.cc threading/post_task_and_reply_impl.cc sequence_checker_impl.cc task_runner.cc sequenced_task_runner.cc thread_task_runner_handle.cc pending_task.cc)

# time
ADD_LIBRARY(time OBJECT third_party/nspr/prtime.cc time/time.cc time/time_posix.cc)

# timer
ADD_LIBRARY(timer OBJECT timer/timer.cc timer/elapsed_timer.cc)

# files
ADD_LIBRARY(files OBJECT files/file.cc files/file_posix.cc files/file_path.cc files/file_path_constants.cc files/file_tracing.cc files/file_enumerator.cc files/file_enumerator_posix.cc files/file_util.cc files/file_util_linux.cc files/file_util_posix.cc files/memory_mapped_file.cc files/memory_mapped_file_posix.cc files/scoped_file.cc path_service.cc)

# metrics
ADD_LIBRARY(metrics OBJECT metrics/histogram.cc metrics/histogram_base.cc metrics/histogram_samples.cc metrics/sparse_histogram.cc metrics/metrics_hashes.cc metrics/sample_map.cc metrics/sample_vector.cc metrics/statistics_recorder.cc metrics/bucket_ranges.cc metrics/field_trial.cc)

# rand_util
ADD_LIBRARY(randutil OBJECT rand_util.cc rand_util_posix.cc)

# hash
ADD_LIBRARY(hash OBJECT third_party/superfasthash/superfasthash.c hash.cc)

# base64
ADD_LIBRARY(base64 OBJECT ../third_party/modp_b64/modp_b64.cc base64.cc base64url.cc)

# md5
ADD_LIBRARY(md5 OBJECT md5.cc)

# sha1
ADD_LIBRARY(sha1 OBJECT sha1_portable.cc)

# values
ADD_LIBRARY(values OBJECT values.cc)

# process
ADD_LIBRARY(process OBJECT process/process_handle.cc process/process_handle_linux.cc process/process_handle_posix.cc process/process_metrics.cc process/process_metrics_linux.cc process/process_metrics_posix.cc process/internal_linux.cc)

# profiler
ADD_LIBRARY(profiler OBJECT location.cc tracked_objects.cc tracking_info.cc profiler/scoped_profile.cc profiler/scoped_tracker.cc profiler/tracked_time.cc profiler/alternate_timer.cc)

# environment
ADD_LIBRARY(environment OBJECT environment.cc)


# all files refer to "base/...", so we include ".." here
SET(include_dirs ${INCLUDE_DIRS} ${libevent_INCLUDE_DIRS} ${icui18n_INCLUDE_DIRS} ${CMAKE_SOURCE_DIR}/..)
SET(link_libraries ${libevent_LIBRARIES} ${icui18n_LIBRARIES} ${CMAKE_THREAD_LIBS_INIT} -lrt -ldl)

ADD_LIBRARY(base SHARED $<TARGET_OBJECTS:switches> $<TARGET_OBJECTS:command_line> $<TARGET_OBJECTS:strings> $<TARGET_OBJECTS:logging> $<TARGET_OBJECTS:i18n> $<TARGET_OBJECTS:debug> $<TARGET_OBJECTS:lock> $<TARGET_OBJECTS:memory> $<TARGET_OBJECTS:messageloop> $<TARGET_OBJECTS:version> $<TARGET_OBJECTS:vlog> $<TARGET_OBJECTS:pickle> $<TARGET_OBJECTS:paths> $<TARGET_OBJECTS:atexit> $<TARGET_OBJECTS:callback> $<TARGET_OBJECTS:lazyinstance> $<TARGET_OBJECTS:posix> $<TARGET_OBJECTS:sysinfo> $<TARGET_OBJECTS:threading> $<TARGET_OBJECTS:time> $<TARGET_OBJECTS:timer> $<TARGET_OBJECTS:files> $<TARGET_OBJECTS:metrics> $<TARGET_OBJECTS:randutil> $<TARGET_OBJECTS:hash> $<TARGET_OBJECTS:base64> $<TARGET_OBJECTS:md5> $<TARGET_OBJECTS:sha1> $<TARGET_OBJECTS:values> $<TARGET_OBJECTS:process> $<TARGET_OBJECTS:profiler> $<TARGET_OBJECTS:environment> nix/xdg_util.cc third_party/xdg_user_dirs/xdg_user_dir_lookup.cc posix/safe_strerror.cc build_time.cc)
INCLUDE_DIRECTORIES(${include_dirs})
TARGET_LINK_LIBRARIES(base ${link_libraries})

INSTALL(TARGETS base
        LIBRARY DESTINATION ${CMAKE_INSTALL_PREFIX}/${CMAKE_INSTALL_LIBDIR}/chromium)