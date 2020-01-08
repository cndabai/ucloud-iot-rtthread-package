import os
from building import *
import rtconfig

cwd  = GetCurrentDir()

src_base  = []

sample_ucloud_mqtt_src  = []
sample_ucloud_mqtt_dynamic_auth_src  = []
sample_ucloud_shadow_src  = []
sample_ucloud_dev_model_src  = []
sample_ucloud_ota_src = []

CPPPATH = []
CPPDEFINES = []
LOCAL_CCFLAGS = ''


#include headfile
CPPPATH += [cwd + '/ports/rtthread']
CPPPATH += [cwd + '/ports/ssl']
CPPPATH += [cwd + '/ports/fal']
CPPPATH += [cwd + '/uiot/certs']
CPPPATH += [cwd + '/uiot/dev_model/include']
CPPPATH += [cwd + '/uiot/mqtt/include']
CPPPATH += [cwd + '/uiot/ota/include']
CPPPATH += [cwd + '/uiot/sdk-impl']
CPPPATH += [cwd + '/uiot/shadow/include']
CPPPATH += [cwd + '/uiot/utils']

#Gen MQTT src file
if GetDepend(['PKG_USING_UCLOUD_MQTT']):
	src_base += Glob('uiot/mqtt/src/*.c')
	src_base += Glob('uiot/utils/*.c')
	src_base += Glob('ports/rtthread/*.c')
	src_base += Glob('ports/fal/*.c')
	SrcRemove(src_base, 'uiot/utils/utils_sha2.c')		

#enable dynamic auth
if GetDepend(['PKG_USING_UCLOUD_MQTT_DYNAMIC_AUTH']):
	CPPDEFINES += ['AUTH_MODE_DYNAMIC']

#Gen shadow src file
if GetDepend(['PKG_USING_UCLOUD_SHADOW']):
	src_base += Glob('uiot/shadow/src/*.c')

#Gen dev model src file
if GetDepend(['PKG_USING_UCLOUD_DEV_MODEL']):
	src_base += Glob('uiot/dev_model/src/*.c')

#Gen ota src file
if GetDepend(['PKG_USING_UCLOUD_OTA']):
	src_base += Glob('uiot/ota/src/*.c')
	
#TLS used
if GetDepend(['PKG_USING_UCLOUD_TLS']):
	src_base += Glob('uiot/certs/ca.c')
	src_base += Glob('ports/ssl/HAL_TLS_mbedtls.c')
	CPPDEFINES += ['SUPPORT_TLS', 'MBEDTLS_CONFIG_FILE=<HAL_TLS_config.h>']	

#Hub C-SDK core
group = DefineGroup('ucloud_iot_sdk', src_base, depend = ['PKG_USING_UCLOUD_IOT_SDK'], CPPPATH = CPPPATH, LOCAL_CCFLAGS = LOCAL_CCFLAGS, CPPDEFINES = CPPDEFINES)

#MQTT Example
if GetDepend(['PKG_USING_UCLOUD_MQTT_SAMPLE']):
	sample_ucloud_mqtt_src += Glob('samples/mqtt/mqtt_sample.c')
	
group = DefineGroup('sample_ucloud_mqtt', sample_ucloud_mqtt_src, depend = ['PKG_USING_UCLOUD_MQTT_SAMPLE'], CPPPATH = CPPPATH, LOCAL_CCFLAGS = LOCAL_CCFLAGS, CPPDEFINES = CPPDEFINES)	

#MQTT Dynamic Auth Example
if GetDepend(['PKG_USING_UCLOUD_MQTT_DYNAMIC_AUTH_SAMPLE']):
	sample_ucloud_mqtt_dynamic_auth_src += Glob('samples/dynamic_auth/dynamic_auth_sample.c')
	
group = DefineGroup('sample_ucloud_mqtt_dynamic_auth', sample_ucloud_mqtt_dynamic_auth_src, depend = ['PKG_USING_UCLOUD_MQTT_DYNAMIC_AUTH_SAMPLE'], CPPPATH = CPPPATH, LOCAL_CCFLAGS = LOCAL_CCFLAGS, CPPDEFINES = CPPDEFINES)	
	
#Shadow Example
if GetDepend(['PKG_USING_UCLOUD_SHADOW_SAMPLE']):
	sample_ucloud_shadow_src += Glob('samples/shadow/shadow_sample.c')
	
group = DefineGroup('sample_ucloud_shadow', sample_ucloud_shadow_src, depend = ['PKG_USING_UCLOUD_SHADOW_SAMPLE'], CPPPATH = CPPPATH, LOCAL_CCFLAGS = LOCAL_CCFLAGS, CPPDEFINES = CPPDEFINES)	

#Dev Model Example
if GetDepend(['PKG_USING_UCLOUD_DEV_MODEL_SAMPLE']):
	sample_ucloud_dev_model_src += Glob('samples/dev_model/dev_model_sample.c')
	
group = DefineGroup('sample_ucloud_dev_model', sample_ucloud_dev_model_src, depend = ['PKG_USING_UCLOUD_DEV_MODEL_SAMPLE'], CPPPATH = CPPPATH, LOCAL_CCFLAGS = LOCAL_CCFLAGS, CPPDEFINES = CPPDEFINES)	

#OTA Example
if GetDepend(['PKG_USING_UCLOUD_OTA_SAMPLE']):
	sample_ucloud_ota_src += Glob('samples/ota/ota_sample.c')
	
group = DefineGroup('sample_ucloud_ota', sample_ucloud_ota_src, depend = ['PKG_USING_UCLOUD_OTA_SAMPLE'], CPPPATH = CPPPATH, LOCAL_CCFLAGS = LOCAL_CCFLAGS, CPPDEFINES = CPPDEFINES)		
  
Return('group')
