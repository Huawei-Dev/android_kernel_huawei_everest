# SPDX-License-Identifier: GPL-2.0
dtb-$(CONFIG_ARCH_HISI) += hi3660-hikey960.dtb
dtb-$(CONFIG_ARCH_HISI) += hi3798cv200-poplar.dtb
dtb-$(CONFIG_ARCH_HISI) += hi6220-hikey.dtb
dtb-$(CONFIG_ARCH_HISI) += hip05-d02.dtb
dtb-$(CONFIG_ARCH_HISI) += hip06-d03.dtb
dtb-$(CONFIG_ARCH_HISI) += hip07-d05.dtb
# Everest EMUI10: compile the original DTS files to individual DTBs first.
# Keep ever_tugl_vh.dtb available for the currently validated single-board boot.
everest_dtb_members := \
	ever_tugl_vc.dtb \
	ever_tugl_vd.dtb \
	ever_lx9_va.dtb \
	ever_tugl_ve.dtb \
	ever_lx9_vb.dtb \
	ever_tugl_vf.dtb \
	ever_lx9_vc.dtb \
	ever_tugl_vg.dtb \
	ever_lx9_vd.dtb \
	ever_tugl_vh.dtb \
	ever_lx9_ve.dtb \
	ever_tugl_vi.dtb \
	ever_lx9_vf.dtb \
	ever_tugl_vj.dtb \
	ever_lx9_vg.dtb

dtb-$(CONFIG_ARCH_HISI) += $(everest_dtb_members)
dtb-$(CONFIG_ARCH_HISI) += everest_catalog.dtb

# Assemble one FDT catalog from the 15 *compiled* DTBs. The Python tool
# validates the per-board identity and uses the kernel-built DTC only to
# pack the catalog; it does not recompile any board DTS file.
quiet_cmd_everest_catalog = EVRCAT  $@
	cmd_everest_catalog = python3 $(srctree)/arch/arm64/boot/dts/hisilicon/make_everest_catalog.py \
	--output $@ --dtc $(DTC) \
	$(foreach m,$(everest_dtb_members),--dtb $(obj)/$(m))

$(obj)/everest_catalog.dtb: $(addprefix $(obj)/,$(everest_dtb_members)) \
	$(srctree)/arch/arm64/boot/dts/hisilicon/make_everest_catalog.py FORCE
	$(call if_changed,everest_catalog)

targets += everest_catalog.dtb

always		:= $(dtb-y)
subdir-y	:= $(dts-dirs)
clean-files	:= *.dtb everest_catalog.dts
