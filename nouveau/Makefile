# $FreeBSD$

SRCDIR=	${.CURDIR:H}/drivers/gpu/drm/nouveau

.PATH:	${SRCDIR} ${SRCDIR}/dispnv04 ${SRCDIR}/dispnv50 ${SRCDIR}/nvif ${SRCDIR}/nvkm

.include "../kconfig.mk"

KMOD=	nouveau
SRCS+=	${SRCDIR}/nouveau_abi16.c \
	${SRCDIR}/nouveau_bios.c \
	${SRCDIR}/nouveau_bo.c \
	${SRCDIR}/nouveau_chan.c \
	${SRCDIR}/nouveau_connector.c \
	${SRCDIR}/nouveau_display.c \
	${SRCDIR}/nouveau_dma.c \
	${SRCDIR}/nouveau_dp.c \
	${SRCDIR}/nouveau_drm.c \
	${SRCDIR}/nouveau_fbcon.c \
	${SRCDIR}/nouveau_fence.c \
	${SRCDIR}/nouveau_gem.c \
	${SRCDIR}/nouveau_hwmon.c \
	${SRCDIR}/nouveau_mem.c \
	${SRCDIR}/nouveau_nvif.c \
	${SRCDIR}/nouveau_prime.c \
	${SRCDIR}/nouveau_sgdma.c \
	${SRCDIR}/nouveau_ttm.c \
	${SRCDIR}/nouveau_usif.c \
	${SRCDIR}/nouveau_vga.c \
	${SRCDIR}/nouveau_vmm.c \
	${SRCDIR}/nv04_fbcon.c \
	${SRCDIR}/nv04_fence.c \
	${SRCDIR}/nv10_fence.c \
	${SRCDIR}/nv17_fence.c \
	${SRCDIR}/nv50_fbcon.c \
	${SRCDIR}/nv50_fence.c \
	${SRCDIR}/nv84_fence.c \
	${SRCDIR}/nvc0_fbcon.c \
	${SRCDIR}/nvc0_fence.c 

# NVIF - HW resource manager
SRCS+=	${SRCDIR}/nvif/client.c \
	${SRCDIR}/nvif/device.c \
	${SRCDIR}/nvif/disp.c \
	${SRCDIR}/nvif/driver.c \
	${SRCDIR}/nvif/fifo.c \
	${SRCDIR}/nvif/mem.c \
	${SRCDIR}/nvif/mmu.c \
	${SRCDIR}/nvif/object.c \
	${SRCDIR}/nvif/user.c \
	${SRCDIR}/nvif/userc361.c \
	${SRCDIR}/nvif/vmm.c
	

.if !empty(KCONFIG:MACPI)
SRCS+=  opt_acpi.h \
	nouveau_acpi.c
.endif

.if !empty(KCONFIG:MCOMPAT)
SRCS+=  nouveau_ioc32.c
.endif

.if !empty(KCONFIG:MDEBUG_FS)
SRCS+=  nouveau_debugfs.c
.endif

.if !empty(KCONFIG:MLEDS_CLASS)
SRCS+=  nouveau_led.c
.endif

.if !empty(KCONFIG:MDRM_NOUVEAU_SVM)
SRCS+=  nouveau_dmem.c \
	nouveau_svm.c
.endif

.if !empty(KCONFIG:MDRM_NOUVEAU_BACKLIGHT)
SRCS+=  nouveau_backlight.c
.endif

.if !empty(KCONFIG:MNOUVEAU_PLATFORM_DRIVER)
SRCS+=  nouveau_platform.c
.endif

CLEANFILES+= ${KMOD}.ko.full ${KMOD}.ko.debug

CFLAGS+= -I${.CURDIR:H}/linuxkpi/gplv2/include
CFLAGS+= -I${.CURDIR:H}/linuxkpi/bsd/include
CFLAGS+= -I${SYSDIR}/compat/linuxkpi/common/include
CFLAGS+= -I${.CURDIR:H}/linuxkpi/dummy/include

CFLAGS+= -I${.CURDIR:H}/include
CFLAGS+= -I${.CURDIR:H}/include/drm
CFLAGS+= -I${.CURDIR:H}/include/uapi
CFLAGS+= -I${SRCDIR:H:H}
CFLAGS+= -I${SRCDIR:H}/nouveau
CFLAGS+= -I${SRCDIR:H}/nouveau/include
CFLAGS+= -I${SRCDIR:H}/nouveau/include/nvif
CFLAGS+= -I${SRCDIR:H}/nouveau/include/nvkm
CFLAGS+= -I${SRCDIR:H}/nouveau/include/nvkm/subdev

CFLAGS+= '-DKBUILD_MODNAME="${KMOD}"'
CFLAGS+= '-DLINUXKPI_PARAM_PREFIX=nouveau_' -DDRM_SYSCTL_PARAM_PREFIX=_${KMOD} -DLINUXKPI_VERSION=50000 -DCONFIG_DRM_NOUVEAU -DCONFIG_NOUVEAU_DEBUG -DCONFIG_NOUVEAU_DEBUG_DEFAULT
CFLAGS+= ${KCONFIG:C/(.*)/-DCONFIG_\1/}

CFLAGS.gcc+= -Wno-redundant-decls -Wno-cast-qual -Wno-unused-but-set-variable \
	-Wno-maybe-uninitialized -Wno-implicit-int]

LDFLAGS+= -Wl,--allow-multiple-definition

SRCS+=	device_if.h vnode_if.h bus_if.h pci_if.h pci_iov_if.h device_if.h iicbus_if.h opt_drm.h \
	opt_vm.h opt_compat.h opt_syscons.h

.include <bsd.kmod.mk>

CWARNFLAGS+= -Wno-format -Wno-unused-but-set-variable -Wno-visibility
CWARNFLAGS+= -Wno-expansion-to-defined -Wno-gnu-variable-sized-type-not-at-end -Wno-incompatible-pointer-types
CWARNFLAGS+=		-Wno-pointer-arith ${CWARNFLAGS.${.IMPSRC:T}}
CWARNFLAGS.nouveau_acpi.c=	-Wno-implicit-function-declaration
CWARNFLAGS.nouveau_abi16.c=	-Wno-unused-variable -Wno-implicit-function-declaration
CWARNFLAGS.nouveau_bios.c=	-Wno-implicit-function-declaration
CWARNFLAGS.nouveau_bo.c=	-Wno-implicit-function-declaration
CWARNFLAGS.nouveau_chan.c=	-Wno-implicit-function-declaration -Wno-unused-variable -Wno-gnu-variable-sized-type-not-at-end
CWARNFLAGS.nouveau_connector.c=	-Wno-implicit-function-declaration -Wno-unused-variable -Wno-int-conversion -Wno-implicit-int -Wno-strict-prototypes -Wno-uninitialized
CWARNFLAGS.nouveau_debugfs.c=	-Wno-int-conversion -Wno-implicit-function-declaration
CWARNFLAGS.nouveau_display.c=	-Wno-int-conversion -Wno-implicit-function-declaration
CWARNFLAGS.nouveau_drm.c=	-Wno-implicit-int -Wno-unused-variable -Wno-int-conversion -Wno-implicit-function-declaration -Wno-implicit-int -Wno-strict-prototypes
CWARNFLAGS.nouveau_fence.c=	-Wno-int-conversion -Wno-implicit-function-declaration
CWARNFLAGS.nouveau_fbcon.c=	-Wno-int-conversion -Wno-implicit-function-declaration -Wno-cast-qual
CWARNFLAGS.nouveau_led.c=	-Wno-int-conversion -Wno-implicit-function-declaration
CWARNFLAGS.nouveau_platform.c=	-Wno-int-conversion -Wno-implicit-function-declaration
CWARNFLAGS.nouveau_svm.c=	-Wno-int-conversion -Wno-implicit-function-declaration
CWARNFLAGS.nouveau_ttm.c=	-Wno-unused-variable
CWARNFLAGS.nv04_fbcon.c=	-Wno-int-conversion -Wno-implicit-function-declaration -Wno-cast-qual
CWARNFLAGS.nv50_fbcon.c=	-Wno-int-conversion -Wno-implicit-function-declaration -Wno-cast-qual
CWARNFLAGS.nvc0_fbcon.c=	-Wno-int-conversion -Wno-implicit-function-declaration -Wno-cast-qual
CWARNFLAGS.event.c=			-Wno-implicit-int -Wno-unused-variable -Wno-int-conversion -Wno-implicit-function-declaration -Wno-implicit-int -Wno-strict-prototypes -Wno-cast-qual
CWARNFLAGS.notify.c=		-Wno-implicit-int -Wno-unused-variable -Wno-int-conversion -Wno-implicit-function-declaration -Wno-implicit-int -Wno-strict-prototypes -Wno-cast-qual
CWARNFLAGS.object.c=		-Wno-implicit-int -Wno-unused-variable -Wno-int-conversion -Wno-implicit-function-declaration -Wno-implicit-int -Wno-strict-prototypes -Wno-cast-qual
CWARNFLAGS.subdev.c=		-Wno-implicit-int -Wno-unused-variable -Wno-int-conversion -Wno-implicit-function-declaration -Wno-implicit-int -Wno-strict-prototypes -Wno-cast-qual

.if ${COMPILER_VERSION} >= 130000
CWARNFLAGS+=   -Wno-error=unused-but-set-variable
.endif
