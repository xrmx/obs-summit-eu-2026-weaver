WEAVER ?= weaver
REGISTRY ?= ./model
DOCS_DIR ?= docs
DOCS_TEMPLATES ?= ./templates

.PHONY: check-model docs live-check

check-model:
	$(WEAVER) registry check --registry $(REGISTRY)

docs: check-model
	$(WEAVER) registry generate \
		--registry $(REGISTRY) \
		--templates "$(DOCS_TEMPLATES)" \
		markdown $(DOCS_DIR)

live-check:
	$(WEAVER) registry live-check --registry $(REGISTRY) --inactivity-timeout 0
