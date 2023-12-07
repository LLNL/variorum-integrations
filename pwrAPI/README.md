PowerAPI Implementation for variorum

List of files {\
	dummy.c (examples)\
	makefile\
	pwrtypes.h (error codes, return types, attribute types, roles)\
	variorum-powerapi.h (main header file)\
}

This implementation is based on the PowerAPI Specification V1.0

This PowerAPI implementation provides a node-level middleware layer between the PowerAPI spec and Variorum.
It is implemented as a header file sitting on top of variorum (links to a pre-built variorum binary).

The main header file variorum-powerapi.h assumes that it sits in a directory within the variorum directory,
ie. "variorum/pwrAPI/variorum-powerapi.h". This headerfile provides the functions and structures that the
user/developer would interact with. pwrtypes.h implements the error codes, return types, roles, and 
object types. These are defined in the powerAPI specifications. you can obtain a copy of the specifications
from the link "https://pwrapi.github.io". *Note that not all types from the specifications are supported 
in this implementation, we only provide a node level implementation at this time, the full set of types
from the reference specs are included for compatibility purposes.

The PowerAPI specifications assume vendor neutrality, as does Variorum. This API wraps the relevant 
Variorum API functions for the supported PowerAPI functions.

An example file called dummy.c is included.

Object obj;\
obj.type = PWR_OBJ_NODE;\
PWR_Time now;\
double value = 0;\
PWR_AttrName type = PWR_ATTR_POWER;\
int ret = PWR_ObjAttrGetValue(&obj, type, &value, &now);

We first create a generic object of type Object, which is then assigned the type that we are interested
in. This type defines the domain of interest. (ie. Node, Socket, Memory, GPU etc.) We then create values 
for PWR_Time, value, and PWR_AttrName (the type of attribute we are interested in for the domain of 
-interest, ie PWR_ATTR_POWER for power). Finally we pass the Object by refernce, attribute type by value,
the return value and PWR_Time by reference. The user recieves the relevant return values in the function 
arguments passed by refernce. This method of interaction is defined by the PowerAPI spec and not a design 
choice.

Currently we support the following types for 

PWR_ObjAttrGetValue:\
	Node-level: Power, Lower bound power limit, Upper bound power limit\
	Memory: Power (for the node)\
	Socket: Power (socket level power consumption including CPU, Memory, GPU - associated with socket)\
PWR_ObjAttrSetValue:\
	Node-level: Power (set power limit for node)



