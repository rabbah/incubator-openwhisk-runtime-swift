OW_USER?=whisk
OW_COMPILER?=$(OW_USER)/action-swift-v4.2
OUT?=../../build/swift4.2
define Build
	cd $(1); \
	docker run -i $(OW_COMPILER) -compile main <./Sources/main.swift >$(OUT)/$(1).zip
endef

define BuildWithLib
	cd $(1); \
	sed -i.bak 's/4.0/4.2/' Package.swift; \
	zip - -r Package.swift Sources/main.swift | docker run -i $(OW_COMPILER) -compile main >$(OUT)/$(1).zip; \
	mv Package.swift.bak Package.swift
endef

Hello:
	$(call Build,HelloSwift4)

HelloCodable:
	$(call Build,HelloSwift4Codable)

Swifty:
	$(call BuildWithLib,SwiftyRequest)

SwiftyCodable:
	$(call BuildWithLib,SwiftyRequestCodable)

Hello5:
	$(call Build,HelloSwift5)

HelloCodable5:
	$(call Build,HelloSwift5Codable)

Swifty5:
	$(call BuildWithLib,SwiftyRequest5)

SwiftyCodable5:
	$(call BuildWithLib,SwiftyRequestCodable5)

all: Hello HelloCodable Swifty SwiftyCodable Hello5 HelloCodable5 Swifty5 SwiftyCodable5

.PHONY: Hello HelloCodable Swifty SwiftyCodable Hello5 HelloCodable5 Swifty5 SwiftyCodable5