TOP = ../..
DEPLOY_CONF := $(TOP)/configure/DEPLOY.conf
PVACCESS_CONSTANTS_CPP_TEMPLATE := $(TOP)/src/pvaccess/pvaccess.constants.cpp.template
SPHINX_CONF := $(TOP)/documentation/sphinx/conf.py

include $(TOP)/configure/CONFIG
#----------------------------------------
#  ADD MACRO DEFINITIONS AFTER THIS LINE

# Global compiler/linker settings

USR_CXXFLAGS += -DPVA_API_VERSION=$(PVA_API_VERSION)
USR_CXXFLAGS += -DPVA_RPC_API_VERSION=$(PVA_RPC_API_VERSION)
USR_CXXFLAGS += -DHAVE_BOOST_NUM_PY=$(HAVE_BOOST_NUM_PY)
USR_CXXFLAGS += -DHAVE_BOOST_PYTHON_NUM_PY=$(HAVE_BOOST_PYTHON_NUM_PY)

USR_CXXFLAGS += $(PVA_PY_CPPFLAGS)
USR_LDFLAGS  += $(PVA_PY_LDFLAGS)
USR_SYS_LIBS += $(PVA_PY_SYS_LIBS)

# Set our library install location; /$(T_A) will be added
INSTALL_LOCATION_LIB = $(INSTALL_LOCATION)/lib/python/$(PYTHON_VERSION)

PVA_PY_VERSION=$(shell cat $(DEPLOY_CONF) | grep PVA_PY_VERSION | cut -f2 -d'=')
ifeq ($(PVA_PY_VERSION),)
    PVA_PY_VERSION=$(shell git rev-parse --short HEAD)
endif


# Expand and install the setup shell scripts

#SCRIPTS_HOST = setup.sh setup.csh setup.full.sh setup.full.csh setup.pythonpath.sh setup.pythonpath.csh 
#SCRIPTS_HOST += $(patsubst ../%@, %, $(wildcard ../setup.*@))
#EXPANDFLAGS += -DPYLIB=$(abspath $(INSTALL_LOCATION_LIB))
#EXPAND += $(SCRIPTS:%=%@)

# Build the Python pvaccess loadable library

LOADABLE_LIBRARY_HOST += pvaccess

# Disable 'lib' prefix
LOADABLE_SHRLIB_PREFIX = 

ifeq ($(OS_CLASS),Darwin)
# Python on Darwin needs the suffix .so
LOADABLE_SHRLIB_SUFFIX = .so
endif


pvaccess_SRCS += pvaccess.cpp

pvaccess_SRCS += pvaccess.constants.cpp
pvaccess_SRCS += pvaccess.PvType.cpp
pvaccess_SRCS += pvaccess.PvProvider.cpp

pvaccess_SRCS += pvaccess.PvObject.cpp
pvaccess_SRCS += pvaccess.PvScalar.cpp
pvaccess_SRCS += pvaccess.PvBoolean.cpp
pvaccess_SRCS += pvaccess.PvByte.cpp
pvaccess_SRCS += pvaccess.PvUByte.cpp
pvaccess_SRCS += pvaccess.PvShort.cpp
pvaccess_SRCS += pvaccess.PvUShort.cpp
pvaccess_SRCS += pvaccess.PvInt.cpp
pvaccess_SRCS += pvaccess.PvUInt.cpp
pvaccess_SRCS += pvaccess.PvLong.cpp
pvaccess_SRCS += pvaccess.PvULong.cpp
pvaccess_SRCS += pvaccess.PvFloat.cpp
pvaccess_SRCS += pvaccess.PvDouble.cpp
pvaccess_SRCS += pvaccess.PvString.cpp
pvaccess_SRCS += pvaccess.PvScalarArray.cpp
pvaccess_SRCS += pvaccess.PvUnion.cpp

pvaccess_SRCS += pvaccess.PvAlarm.cpp
pvaccess_SRCS += pvaccess.PvTimeStamp.cpp

pvaccess_SRCS += pvaccess.NtType.cpp
pvaccess_SRCS += pvaccess.NtTable.cpp

pvaccess_SRCS += pvaccess.Channel.cpp
pvaccess_SRCS += pvaccess.RpcClient.cpp
pvaccess_SRCS += pvaccess.RpcServer.cpp

pvaccess_SRCS += pvaccess.ScalarArrayPyOwner.cpp

pvaccess_SRCS += CaClient.cpp
pvaccess_SRCS += Channel.cpp
pvaccess_SRCS += ChannelGetRequesterImpl.cpp
pvaccess_SRCS += ChannelMonitorRequesterImpl.cpp
pvaccess_SRCS += ChannelPutRequesterImpl.cpp
pvaccess_SRCS += ChannelRequesterImpl.cpp
#pvaccess_SRCS += ChannelRpcServiceImpl.cpp
pvaccess_SRCS += ChannelTimeout.cpp
pvaccess_SRCS += FieldNotFound.cpp
pvaccess_SRCS += GetFieldRequesterImpl.cpp
pvaccess_SRCS += InvalidArgument.cpp
pvaccess_SRCS += InvalidDataType.cpp
pvaccess_SRCS += InvalidRequest.cpp
pvaccess_SRCS += InvalidState.cpp
pvaccess_SRCS += NtTable.cpp
pvaccess_SRCS += NtType.cpp
pvaccess_SRCS += ObjectAlreadyExists.cpp
pvaccess_SRCS += ObjectNotFound.cpp
pvaccess_SRCS += PvaClient.cpp
pvaccess_SRCS += PvaConstants.cpp
pvaccess_SRCS += PvaException.cpp
pvaccess_SRCS += PvaExceptionTranslator.cpp
pvaccess_SRCS += PvaPyLogger.cpp
pvaccess_SRCS += PvAlarm.cpp
pvaccess_SRCS += PvBoolean.cpp
pvaccess_SRCS += PvByte.cpp
pvaccess_SRCS += PvDouble.cpp
pvaccess_SRCS += PvFloat.cpp
pvaccess_SRCS += PvInt.cpp
pvaccess_SRCS += PvLong.cpp
pvaccess_SRCS += PvObject.cpp
pvaccess_SRCS += PvProvider.cpp
pvaccess_SRCS += PvScalar.cpp
pvaccess_SRCS += PvScalarArray.cpp
pvaccess_SRCS += PvShort.cpp
pvaccess_SRCS += PvString.cpp
pvaccess_SRCS += PvTimeStamp.cpp
pvaccess_SRCS += PvUByte.cpp
pvaccess_SRCS += PvUInt.cpp
pvaccess_SRCS += PvULong.cpp
pvaccess_SRCS += PvUnion.cpp
pvaccess_SRCS += PvUShort.cpp
pvaccess_SRCS += PvUtility.cpp
pvaccess_SRCS += PyGilManager.cpp
pvaccess_SRCS += PyPvDataUtility.cpp
pvaccess_SRCS += PyUtility.cpp
pvaccess_SRCS += RequesterImpl.cpp
#pvaccess_SRCS += RpcChannelImpl.cpp
#pvaccess_SRCS += RpcChannelProviderFactory.cpp
#pvaccess_SRCS += RpcChannelProviderImpl.cpp
pvaccess_SRCS += RpcClient.cpp
#pvaccess_SRCS += RpcServerContextImpl.cpp
pvaccess_SRCS += RpcServiceImpl.cpp
pvaccess_SRCS += RpcServer.cpp
pvaccess_SRCS += RpcTimeout.cpp
pvaccess_SRCS += StringUtility.cpp

with_pvaClient := $(shell $(PERL) -e "print $(PVA_API_VERSION) >= 450")
pvaccess_1_SRCS += pvaccess.PvaServer.cpp
pvaccess_1_SRCS += PvaServer.cpp
pvaccess_1_SRCS += PyPvRecord.cpp
pvaccess_SRCS += $(pvaccess_$(with_pvaClient)_SRCS)

pvaccess_1_LIBS += pvaClient
pvaccess_1_LIBS += nt
pvaccess_1_LIBS += pvDatabase
pvaccess_LIBS += $(pvaccess_$(with_pvaClient)_LIBS)

pvaccess_LIBS += pvAccess
pvaccess_LIBS += pvData
pvaccess_LIBS += Com


# Build test clients on Linux

#TESTPROD_HOST_Linux += testPvaPyClient
#LIBRARY_HOST += pvaccess
#testPvaPyClient_LIBS += pvaccess
#testPvaPyClient_LIBS += pvAccess
#testPvaPyClient_LIBS += pvData
#testPvaPyClient_LIBS += Com

#TESTPROD_HOST_Linux += testPvaClient
#testPvaClient_LIBS += pvaClient
#testPvaClient_LIBS += pvAccess
#testPvaClient_LIBS += pvData
#testPvaClient_LIBS += Com

include $(TOP)/configure/RULES
#----------------------------------------
#  ADD RULES AFTER THIS LINE

pvaccess.constants.cpp: $(PVACCESS_CONSTANTS_CPP_TEMPLATE) $(DEPLOY_CONF)
	eval "cat ${PVACCESS_CONSTANTS_CPP_TEMPLATE} | sed 's?PVA_PY_VERSION?${PVA_PY_VERSION}?g' > pvaccess.constants.cpp"
	eval "cat ${SPHINX_CONF} | sed 's?version =.*?version = \"${PVA_PY_VERSION}\"?g' | sed 's?release =.*?release = \"${PVA_PY_VERSION}\"?g' > ${SPHINX_CONF}.2 && mv ${SPHINX_CONF}.2 ${SPHINX_CONF}"

