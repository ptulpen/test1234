# Copyright (c) 2010 Fizians SAS. <http://www.fizians.com>
# This file is part of Rozofs.
#
# Rozofs is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published
# by the Free Software Foundation, version 2.
#
# Rozofs is distributed in the hope that it will be useful, but
# WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
# General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program.  If not, see
# <http://www.gnu.org/licenses/>.


add_definitions(-DD_REENTRANT -D_FILE_OFFSET_BITS=64)
include_directories(${CMAKE_BINARY_DIR}) # for config.h
include_directories(${CMAKE_SOURCE_DIR}) # for librozofs headers
include_directories(${PTHREAD_INCLUDE_DIR})
link_directories(${CMAKE_BINARY_DIR}/rozofs)

add_executable(exportd
    volume.h
    volume.c
    mreg.h
    mreg.c
    mdir.h
    mdir.c
    mslnk.h
    mslnk.c
    dirent_journal.h
    mdirent.h
    dirent_file_repair.c
    writeback_cache.c
    dirent_file.c
    dirent_cache.c
    dirent_search.c
    dirent_insert.c
    dirent_enum2String_file_repair_cause_e.h
    cache.h
    cache.c
    exp_cache.c
    exp_cache.h
    export.h
    export_tracking.c
    eproto.c
    monitor.h
    monitor.c
    econfig.h
    econfig.c
    exportd.c
    exp_cache_dirty_mgt.c
    export_expgw_conf.c
    export_expgw_conf.h
    export_internal_channel.c
    export_internal_channel.h
    export_nblock_init.c
    export_expgateway_conf.c
    export_expgateway_conf.h
    export_expgateway_sup.c
    export_gwprotoclt.c      
    eproto_nb.c
    eproto_nb.h    
    export_north_intf.c     
    export_share.c     
    export_share.h     
    eprotosvc_nb.c
   xattr_acl.c
   xattr_main.c
   xattr_nocache.c
   xattr_security.c
   xattr_stub.c
   xattr_system.c
   xattr_trusted.c
   xattr_user.c
   exp_cache.h
   rozofs_ext4.h
   xattr.h
   xattr_main.h
   export_tracking_poll.c
   dirent_writeback_cache.c
   export_trash_reload.c
    geo_replication.c
    geo_replication_dbg.c    
    geo_replication.h
    
    geo_replica_proto_nb.c    
    geo_replica_proto_nb.h
    geo_replica_protosvc_nb.h   
    geo_replica_protosvc_nb.c   
    geo_replica_srv.c
    geo_replica_srv.h
    geo_replica_north_intf.c
    geo_replica_north_intf.h
    geo_replica_ctx.c
    geo_replica_ctx.h
    geo_replica_tmr.c
    geo_replica_tmr.h

    rozofs_quota.h
    rozofs_quota_api.h
    rozofs_quota.c
    quota_writeback_cache.c
    export_quota_thread.c
    rozofs_quota_intf_srv_thread.c        
)
target_link_libraries(exportd rozofs ${PTHREAD_LIBRARY} ${UUID_LIBRARY} ${CONFIG_LIBRARY})


#add_executable(expgateway
#    expgw_attr_cache.c
#    expgw_attr_cache.h
#    expgw_eprotosvc.c
#    expgw_export.h
#    expgw_fid_cache.c
#    expgw_fid_cache.h
#    expgw_lookup.c
#    expgw_attr.c
#    expgw_create_dir_file.c
#    expgw_delete_dir_file.c
#    expgw_mgt.c
#    expgw_rozofs_north_intf.c
#    expgw_send.c
#    expgw_proto.h
#    expgw_exportd_north_intf.c
#    expgw_main.c
#    expgw_main.h
#    expgw_nblock_init.c
#    expgw_gwprotosvc.c
#    expgw_gwprotosvc.h
#    expgw_gw_poll.c
#)
#target_link_libraries(expgateway rozofs ${PTHREAD_LIBRARY} ${UUID_LIBRARY} ${CONFIG_LIBRARY})



add_executable(rozo_repquota
    rozofs_quota.h
    rozofs_quota.c
    rozofs_quota_api.h
    quota_writeback_cache.c
    rozofs_repquota.c
    econfig.h
    econfig.c
)
target_link_libraries(rozo_repquota rozofs ${PTHREAD_LIBRARY} ${UUID_LIBRARY} ${CONFIG_LIBRARY})

add_executable(rozo_setquota
    rozofs_quota.h
    rozofs_quota.c
    rozofs_quota_api.h
    quota_writeback_cache.c
    rozofs_setquota.c
    rozofs_quota_intf.h
    rozofs_quota_util.c
    econfig.h
    econfig.c
)
target_link_libraries(rozo_setquota rozofs ${PTHREAD_LIBRARY} ${UUID_LIBRARY} ${CONFIG_LIBRARY})


add_executable(rozo_quotaon
    rozofs_quota.h
    rozofs_quota.c
    rozofs_quota_api.h
    quota_writeback_cache.c
    rozofs_quotaon.c
    rozofs_quota_intf.h
    rozofs_quota_util.c
    econfig.h
    econfig.c
)
target_link_libraries(rozo_quotaon rozofs ${PTHREAD_LIBRARY} ${UUID_LIBRARY} ${CONFIG_LIBRARY})

add_executable(rozo_warnquota
    rozofs_quota.h
    rozofs_quota.c
    rozofs_quota_api.h
    quota_writeback_cache.c
    rozofs_warnquota.c
    rozofs_quota_intf.h
    rozofs_quota_util.c
    econfig.h
    econfig.c
)
target_link_libraries(rozo_warnquota rozofs ${PTHREAD_LIBRARY} ${UUID_LIBRARY} ${CONFIG_LIBRARY})
set (librozo_inode_sources
       cache.c
       exp_cache.c
       exp_cache.h
       mdirent.h
       dirent_file_repair.c
       dirent_writeback_cache.c
       writeback_cache.c
       dirent_file.c
       dirent_cache.c
       dirent_insert.c
       dirent_search.c
       test_mdirent_stub.c
       rozo_inode_lib.c
       rozo_inode_lib.h

)
add_library(rozofs_inode STATIC ${librozo_inode_sources})
set_target_properties(rozofs_inode PROPERTIES COMPILE_FLAGS "-fPIC")


#add_executable(rzsave
#    rzsave_main.c  
#)
#target_link_libraries(rzsave rozofs_inode rozofs ${PTHREAD_LIBRARY} ${UUID_LIBRARY} ${CONFIG_LIBRARY})


#________________________________________________________
# Translate a FID or a list of FIDs from a file into a 
# full file name
#
add_executable(rozo_fid2pathname
    rozo_fid2pathname.c  
)
target_link_libraries(rozo_fid2pathname rozofs_inode rozofs ${PTHREAD_LIBRARY} ${UUID_LIBRARY} ${CONFIG_LIBRARY})


#________________________________________________________
add_executable(rozo_clusterstats
    rozo_clusterstats.c  
)
target_link_libraries(rozo_clusterstats rozofs_inode rozofs ${PTHREAD_LIBRARY} ${UUID_LIBRARY} ${CONFIG_LIBRARY})


#________________________________________________________
add_executable(rozo_buildfid_list
    rozo_fidlist_from_cidsid.c  
    econfig.c  
)
target_link_libraries(rozo_buildfid_list rozofs_inode rozofs ${PTHREAD_LIBRARY} ${UUID_LIBRARY} ${CONFIG_LIBRARY})


#________________________________________________________
# Build lists of FID information for the rebuild process
# of a whole storage or a whole cid/sid
#
add_executable(rozo_rbsList
    rozo_rbsList.c  
    econfig.c  
)
target_link_libraries(rozo_rbsList rozofs_inode rozofs ${PTHREAD_LIBRARY} ${UUID_LIBRARY} ${CONFIG_LIBRARY})

#________________________________________________________
# Build lists of FID of an export for geo replication from 
# scratch
#
add_executable(rozo_geoRepList
    rozo_geoRepList.c  
    econfig.c  
)
target_link_libraries(rozo_geoRepList rozofs_inode rozofs ${PTHREAD_LIBRARY} ${UUID_LIBRARY} ${CONFIG_LIBRARY})


# Install
install(CODE "EXECUTE_PROCESS (COMMAND mkdir -p ${ROZOFS_CONFIG_DIR})" COMPONENT export)

install(TARGETS exportd
    RUNTIME DESTINATION bin
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib
    COMPONENT export
)
install(TARGETS rozo_warnquota
    RUNTIME DESTINATION bin
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib
    COMPONENT rozo_warnquota
)
install(TARGETS rozo_setquota
    RUNTIME DESTINATION bin
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib
    COMPONENT rozo_setquota
)
install(TARGETS rozo_repquota
    RUNTIME DESTINATION bin
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib
    COMPONENT rozo_repquota
)
install(TARGETS rozo_quotaon
    RUNTIME DESTINATION bin
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib
    COMPONENT rozo_quotaon
)

install(TARGETS rozo_fid2pathname
    RUNTIME DESTINATION bin
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib
    COMPONENT rozo_fid2pathname
)

install(TARGETS rozo_clusterstats
    RUNTIME DESTINATION bin
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib
    COMPONENT rozo_clusterstats
)

install(TARGETS rozo_buildfid_list
    RUNTIME DESTINATION bin
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib
    COMPONENT rozo_buildfid_list
)

install(TARGETS rozo_rbsList
    RUNTIME DESTINATION bin
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib
    COMPONENT rozo_rbsList
)

install(TARGETS rozo_geoRepList
    RUNTIME DESTINATION bin
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib
    COMPONENT rozo_geoRepList
)
install(FILES export.conf.sample DESTINATION ${ROZOFS_CONFIG_DIR} COMPONENT export)
install(FILES export.conf DESTINATION ${ROZOFS_CONFIG_DIR} COMPONENT export)
install(PROGRAMS rozo_geoReplicationReinitialize.sh DESTINATION bin)
