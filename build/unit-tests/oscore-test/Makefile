###############################################################################
# File: OSAL Application Makefile 
#
#
# History:
#
###############################################################################

include ../../osal-config.mak

#
# Subsystem produced by this makefile.
#
APPTARGET = oscore-test

#
# Unit test object files 
#
OBJS = ut_oscore_task_test.o ut_oscore_binsem_test.o ut_oscore_mutex_test.o \
       ut_oscore_countsem_test.o ut_oscore_queue_test.o ut_oscore_misc_test.o 


ifeq ($(OS), vxworks6)
#
# Unit test object files specific to vxWorks platforms
#
    OBJS += ut_oscore_exception_test.o ut_oscore_interrupt_test.o \
        ut_oscore_test_vxworks.o
        
else
# assume Linux as the default
#
# Unit test object files specific to Linux platforms
#
    OBJS += ut_oscore_test.o

endif
    

#
# Core object files
# 
OBJS += osapi.o osfileapi.o osfilesys.o osloader.o osnetwork.o ostimer.o

#
# BSP Object files
#
OBJS += bsp_ut_voltab.o bsp_ut.o

#
# UT Assert files
#
OBJS += utassert.o utlist.o utstubs.o uttest.o uttools.o

#
# Unit test shared object files
# 
OBJS += ut_os_stubs.o

#
# Source files required to build subsystem; used to generate dependencies.
# As long as there are no assembly files this can be automated.
#
SOURCES = $(OBJS:.o=.c)

#
# Specify extra C Flags needed to build this subsystem
#
#LOCAL_COPTS = -DUT_OS_USE_ATA
LOCAL_COPTS = -DUT_OS_USE_RAM

#
# EXEDIR is defined here, just in case it needs to be different for a custom build
#
EXEDIR =./

########################################################################
# Should not have to change below this line, except for customized 
# directory structures
########################################################################

#
# no core objects, since all objs for unit tests are built in this directory 
#
CORE_OBJS = 

# 
# Include all necessary make rules
# Any of these can be copied to a local file and changed if needed.
#

#
#       osal-config.mak contians arch, BSP, and OS selection
#
include ../../osal-config.mak

#
#       debug-opts.mak contains debug switches
#
include ../../debug-opts.mak

#
#       compiler-opts.mak contains compiler definitions and switches/defines
#
include $(OSAL_SRC)/bsp/$(BSP)/make/compiler-opts.mak

#
# Setup the include path for this subsystem
# The OS specific includes are in the build-rules.make file
#

#
# If this subsystem needs include files from another app, add the path here.
#
INCLUDE_PATH  = -I$(OSAL_SRC)/inc
INCLUDE_PATH += -I$(OSAL_SRC)/os/inc
INCLUDE_PATH += -I$(OSAL_SRC)/unit-tests/shared
INCLUDE_PATH += -I$(OSAL_SRC)/unit-tests/$(APPTARGET)
INCLUDE_PATH += -I$(OSAL_SRC)/../ut_assert/inc
INCLUDE_PATH += -I../../inc

#
# Define the VPATH make variable. 
# This can be modified to include source from another directory.
# If there is no corresponding app in the apps directory, then this can be discarded, or
# if the mission chooses to put the src in another directory such as "src", then that can be 
# added here as well.
#
VPATH =  $(OSAL_SRC)/unit-tests/$(APPTARGET)
VPATH += $(OSAL_SRC)/unit-tests/shared
VPATH += $(OSAL_SRC)/os/$(OS)
VPATH += $(OSAL_SRC)/bsp/$(BSP)/ut-src
VPATH += $(OSAL_SRC)/../ut_assert/src

#
# Include the common make rules for building an OSAL Application
#
include $(OSAL_SRC)/make/app-rules.mak

