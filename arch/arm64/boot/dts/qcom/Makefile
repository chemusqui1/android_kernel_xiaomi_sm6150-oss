# SPDX-License-Identifier: GPL-2.0
ifeq ($(CONFIG_BUILD_ARM64_DT_OVERLAY),y)
	dtbo-$(CONFIG_MACH_XIAOMI_DAVINCI) += \
		davinci-sdmmagpie-overlay.dtbo \
		davinci_m0a-sdmmagpie-overlay.dtbo \
		davinci_m0b-sdmmagpie-overlay.dtbo
	davinci-sdmmagpie-overlay.dtbo-base := sdmmagpie.dtb
	davinci_m0a-sdmmagpie-overlay.dtbo-base := sdmmagpie.dtb
	davinci_m0b-sdmmagpie-overlay.dtbo-base := sdmmagpie.dtb

	dtbo-$(CONFIG_MACH_XIAOMI_PHOENIX) += \
		phoenix-sdmmagpie-overlay.dtbo
	phoenix-sdmmagpie-overlay.dtbo-base := sdmmagpie.dtb

	dtbo-$(CONFIG_MACH_XIAOMI_TOCO) += \
		toco-sdmmagpie-overlay.dtbo
	toco-sdmmagpie-overlay.dtbo-base := sdmmagpie.dtb

	dtbo-$(CONFIG_MACH_XIAOMI_TUCANA) += \
		tucana-sdmmagpie-overlay.dtbo
	tucana-sdmmagpie-overlay.dtbo-base := sdmmagpie.dtb
else
dtb-$(CONFIG_ARCH_SDMMAGPIE)	+= \
	davinci-sdmmagpie.dtb \
	davinci_m0a-sdmmagpie.dtb \
	davinci_m0b-sdmmagpie.dtb \
	tucana-sdmmagpie.dtb \
	toco-sdmmagpie.dtb \
	phoenix-sdmmagpie.dtb
endif

ifeq ($(CONFIG_ARM64),y)
always		:= $(dtb-y)
subdir-y	:= $(dts-dirs)
else
targets += dtbs
targets += $(addprefix ../, $(dtb-y))

$(obj)/../%.dtb: $(src)/%.dts FORCE
	$(call if_changed_dep,dtc)

ifeq ($(CONFIG_BUILD_ARM64_DT_OVERLAY),y)
$(obj)/%.dtbo:$(src)/../../../../arm64/boot/dts/qcom/%.dts FORCE
	$(call if_changed_dep,dtc)
	$(call if_changed,dtbo_verify)

dtbs: $(addprefix $(obj)/,$(dtb-y)) $(addprefix $(obj)/,$(dtbo-y))
else
dtbs: $(addprefix $(obj)/../,$(dtb-y))
endif
endif
clean-files	:= *.dtb *.dtbo
