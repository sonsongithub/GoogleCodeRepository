INFOPLIST_FILE=Info.plist
SOURCES=\
	main.m \
	MyApp.m

CC=/usr/local/arm-apple-darwin/bin/gcc
CFLAGS=-g -O2 -Wall
LD=$(CC)
LDFLAGS=-Wl,-syslibroot,/usr/local/arm-apple-darwin/heavenly -lobjc -ObjC -framework CoreFoundation -framework Foundation -framework CoreGraphics -framework GraphicsServices -framework UIKit -framework LayerKit

WRAPPER_NAME=$(PRODUCT_NAME).app
EXECUTABLE_NAME=$(PRODUCT_NAME)
SOURCES_ABS=$(addprefix $(SRCROOT)/,$(SOURCES))
INFOPLIST_ABS=$(addprefix $(SRCROOT)/,$(INFOPLIST_FILE))
OBJECTS=\
	$(patsubst %.c,%.o,$(filter %.c,$(SOURCES))) \
	$(patsubst %.cc,%.o,$(filter %.cc,$(SOURCES))) \
	$(patsubst %.cpp,%.o,$(filter %.cpp,$(SOURCES))) \
	$(patsubst %.m,%.o,$(filter %.m,$(SOURCES))) \
	$(patsubst %.mm,%.o,$(filter %.mm,$(SOURCES)))
OBJECTS_ABS=$(addprefix $(CONFIGURATION_TEMP_DIR)/,$(OBJECTS))
APP_ABS=$(BUILT_PRODUCTS_DIR)/$(WRAPPER_NAME)
PRODUCT_ABS=$(APP_ABS)/$(EXECUTABLE_NAME)

all: $(PRODUCT_ABS)

$(PRODUCT_ABS): $(APP_ABS) $(OBJECTS_ABS)
	$(LD) $(LDFLAGS) -o $(PRODUCT_ABS) $(OBJECTS_ABS)

$(APP_ABS): $(INFOPLIST_ABS)
	mkdir -p $(APP_ABS)
	cp $(INFOPLIST_ABS) $(APP_ABS)/
	cp $(SRCROOT)/$(RESOURCES)/*.png $(APP_ABS)/

$(CONFIGURATION_TEMP_DIR)/%.o: $(SRCROOT)/%.m
	mkdir -p $(dir $@)
	$(CC) $(CFLAGS) $(CPPFLAGS) -c $< -o $@

clean:
	echo rm -f $(OBJECTS_ABS)
	echo rm -rf $(APP_ABS)

