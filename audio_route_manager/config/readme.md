Audio Route Manager Configuration

==================================

This configuration is given as an example but each platform implementor must provide his own set
of configuration file.

Parameter Framework Criterion type, criteria definition and rogue parameters for
intel platforms.
This configuration file is mostly for the definition of the elements of the PFW and their
link with Android Events such as parameters.
For more documentation on the PFW, please refer to the github link:

https://github.com/01org/parameter-framework


==================================
Rogue Parameter Example:

 Note that wrapping table is not mandatory.
 When the parameter structure is declared as an array and only one parameter value
 is received from the client (e.g for volume controls), that value will
 be duplicated before being broadcasted. This will ensure consistency with the alsa mapping.

    <rogue_parameter name="<volume_amp_media_front>" type="<string|uint32_t|double>"
                     default="<default value in the PFW parameter domain>"
                     parameter="<associated Android Parameter key>"
                     path="<Path of the rogue parameter>"
                     mapping="<Android Param 1, PFW Param 1>,<Android Param 2, PFW Param 2>,...>">
    </rogue_parameter>

==================================
Criterion type Example:

 For each criterion, a couple of numerical, literal values must be provided to the PFW.
 The numerical part is not mandatory. If not filled by the user, a default numerical value will be
 automatically provided by audio HAL using the following logic:
   - Exclusive criterion:
          * 0 -> first literal value,
          * 1 -> second literal value,
               ...
          * N -> (N+1)th literal value.
   - Inclusive criterion:
          * 1 << 0 -> first literal value,
          * 1 << 1 -> second literal value,
               ...
          * 1 << N -> (N+1)th literal value,

    <criterion_type name="<Criterion Name>" type="<exclusive|inclusive>"
                values="<[numerical value 1:]<literal value 1>,[numerical value 2:]<literal value 2>,<literal value 3>>">
    </criterion_type>


==================================
Criterion:

 Note that parameter and mapping are not mandatory.
 If given, it means that this criterion is associated to an Android Parameter Example:
 If not, the criterion is standalone.

    <criterion name="<Criterion Name>" type="<Criterion type name>" parameter="<associated Android Parameter key>" default="<default value of the criterion>"
               mapping="< <Android Param 1, PFW Criterion Value 1>,...>">
    </criterion>
