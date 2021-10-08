# QMK Files for ARTSEY

# How to Build:

## Step 1. Set up QMK.

### Setup QMK According to the Official Guide. 

*Make sure you update your QMK if you are using an older version. Features that make ARTSEY possible were added on August, 29, 2021.*

https://beta.docs.qmk.fm/tutorial/newbs_getting_started

## Step 2. Place files of choosen artseyio type (left or right-handed) in QMK `keyboards/` directory. 

Copy choosen type folder to `<QMK_home>/keyboards/`

## Step 3. Make sure Combos and Mousekeys are enabled in rules.h of your keyboard.  
Add these lines to your `rules.mk`

	COMBO_ENABLE = yes
	MOUSEKEYS_ENABLE = yes

## Step 4. Copy these files into the /keyboards/your_keyboard/ folder
These files are found in either the /left_hand or /right_hand folder of this repo. Chose the files from the folder that correspond to whether you are using the left- or right-hand layout. 

	artsey.c  
	artsey.h
	artsey_basic.def
	combos.def
	keymap_combo.h
	macros.c

## Step 5. Customize your keymap if you need it.   
### Make sure you have all necessary Includes
Include this somewhere near the top of your keymap:  

	#include "artsey.h"
	#include "keymap_combo.h"
	#include "artsey.c"

### Base, Number, Nav, Symbol, Bracket, Mouse, and Custom Layers. 

There are 7 default layers: `_A_BASE`,` _A_NUM`,` _A_NAV`,` _A_SYM`,` _A_BRAC`,` _A_MOU` and `_A_CUSTOM`. 

You will need to make sure these 7 layers are created on your keyboard and the 8 artsey keycodes are maped on each layer. The keycodes are of the form:

	A_LAYER_A
	A_LAYER_R
	A_LAYER_T
	A_LAYER_S
	A_LAYER_E
	A_LAYER_Y
	A_LAYER_I
	A_LAYER_O
	
### Full Example

Default keymap examples are avalable in each folder. An example keymap for an 8-key right handed board might look like this:

	//REPLACE THIS WITH YOUR KEYBOARD.h 
	#include "keyboard.h"

	//MAKE SURE THESE ARE INCLUDED
	#include "artsey.h"
	#include "keymap_combo.h"
	#include "artsey.c"

	const uint16_t PROGMEM keymaps[][MATRIX_ROWS][MATRIX_COLS] = {

	[_A_BASE] = LAYOUT(A_BASE_A,A_BASE_R,A_BASE_T,A_BASE_S,
	A_BASE_E,A_BASE_Y,A_BASE_I,A_BASE_O),

	[_A_NUM] = LAYOUT(A_NUM_A,A_NUM_R,A_NUM_T,A_NUM_S,
	A_NUM_E,A_NUM_Y,A_NUM_I,A_NUM_O),

	[_A_NAV] = LAYOUT(A_NAV_A,A_NAV_R,A_NAV_T,A_NAV_S,
	A_NAV_E,A_NAV_Y,A_NAV_I,A_NAV_O),

	[_A_SYM] = LAYOUT(A_SYM_A,A_SYM_R,A_SYM_T,A_SYM_S,
	A_SYM_E,A_SYM_Y,A_SYM_I,A_SYM_O),

	[_A_BRAC] = LAYOUT(A_BRAC_A,A_BRAC_R,A_BRAC_T,A_BRAC_S,
	A_BRAC_E,A_BRAC_Y,A_BRAC_I,A_BRAC_O),

	[_A_MOU] = LAYOUT(A_MOU_A,A_MOU_R,A_MOU_T,A_MOU_S,
	A_MOU_E,A_MOU_Y,A_MOU_I,A_MOU_O),

	[_A_CUSTOM] = LAYOUT(A_CUSTOM_A,A_CUSTOM_R,A_CUSTOM_T,A_CUSTOM_S,
	A_CUSTOM_E,A_CUSTOM_Y,A_CUSTOM_I,A_CUSTOM_O),


	};


For a left handed layout, simply mirror-image the keycodes. For instance, the base layer would look like (see the file in the /left_hand/keymaps/artsey_left/ folder for a full example:

	[_A_BASE] = LAYOUT(A_BASE_S,A_BASE_T,A_BASE_R,A_BASE_A,
	A_BASE_O,A_BASE_I,A_BASE_Y,A_BASE_E),
	
## Step 6 (Optional). Add some suggested behavior to `config.h`.

### To modify the combo term to your liking. 
Add this to your `config.h`:  
	
	#define COMBO_TERM 200
	
For new users, start with 200. Reduce this as you get faster. 

### To enable locking the one-shot mods by tapping them three times. 
Add this to your `config.h`:  

	#define ONESHOT_TAP_TOGGLE 3 

### To enable time-out for one-shot mods. 
Add this to your `config.h`:  

	#define ONESHOT_TIMEOUT 5000 
	
### To improve the behavior of mousekeys.
Add this to your `config.h`:  
	
	#define MOUSEKEY_INTERVAL 12
  	#define MOUSEKEY_MAX_SPEED 6
  	#define MOUSEKEY_TIME_TO_MAX 50
  	#define MOUSEKEY_DELAY 20
	
### To improve the behavior of layer-tap keys.
Add this to your `config.h`  
	
	#define TAPPING_TERM 200
	#define PERMISSIVE_HOLD
	#define IGNORE_MOD_TAP_INTERRUPT
	

# How to Modify:

All of the ARTSEY combo behavior is defined in `macros.c`. The non-combo key behavior is defined in `artsey.h`. These files are autogenerated by `generator.R` using the comma-separated definition files in `artsey_combos.csv` and `artsey_keycodes.csv`. To chang ARTSEY, make modifications to these files, save them, and run `generator.R`. You can also use an online version of the generator at http://keyboardlist.com