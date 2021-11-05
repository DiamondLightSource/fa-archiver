# This make file is designed to be called from the top level make file
ifndef PYTHON_BUILD_DIR
$(error Do not call this make file directly)
endif

DIST_DIR = $(PYTHON_BUILD_DIR)/dist

PYTHON_SHORT_VERSION = 2.7
PYTHON_SHORT_VERSION = $(shell \
    $(PYTHON) --version 2>&1 | grep -oP '(?<=^Python )[^.]*\.[^.]*')


# This is run when we type make
dist: setup.py $(shell find -name \*.py)
	$(PYTHON) setup.py bdist_egg --dist-dir $(DIST_DIR)
	rm -rf build

# Clean the module
clean:
	find -name '*.pyc' -exec rm {} \;
	rm -rf build fa_archiver.egg-info installed.files

# Install the built egg and keep track of what was installed
install: $(DIST_DIR)
	mkdir -p $(PREFIX)/lib/python$(PYTHON_SHORT_VERSION)/site-packages
	$(PYTHON) setup.py easy_install -m \
            --record=installed.files \
            --prefix=$(PREFIX) $(DIST_DIR)/*.egg
