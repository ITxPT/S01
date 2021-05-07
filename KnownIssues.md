# S01 Know Issues list #
This document contains know issues for the ITxPT 2.1.1 S01 specification. It contains items that someone implementing towards the relevant part of the specification could potentially benefit of being aware of. Items that falls outside of this, e.g. requests for an additional feature are not part of this document.

The expectation is that these issues will be addressed in a future revision of the specification. There is no guarantee that that future specification revision will be in line with implementation advice below; implementation advice is a best-effort attempt to outline something that will cause the least amount of problems and/or are most likely to be in line with a future specification update. The implementation advice may change without notice!

# S01 Known Issues #

### Section 1.1 “Architecture requirements” ###
**Issue:** First states that “To build an ITxPT compliant onboard architecture, the minimum and mandatory network features and services are:” with a list of features and services. Then below that list it is stated that “The above target can be implemented step-by-step,…”. This can seem contradictory.

**Implementation advice:** What is meant is that a fully ITxPT compliant vehicle needs to have all of these parts. It is allowed/possible to have an ITxPT compliant vehicle and several ITxPT compliant modules/services that don’t reach the level of fully compliant. 

### Section 2.4.1.3 “Wireless communication cables” ###
**Issue:** States that “Cables from antennas are connected directly to the dedicated modules if available with specified connectors. If modules are not available, specified connectors are predisposed at cable end with a reasonable cable length reserve (50cm) from the input of the enclosure, in order to ensure connectivity with the ITS module in charge of related feature.” This leaves undefined how much cable length reserve there should be when the module is present.

**Implementation advice:** If the module is already present, the full 50 cm may not be necessary. But there should be sufficient cable length reserve so that minor changes in connector placement – e.g., a different VCG with connectors in a different location, is possible. 

### Section 2.1.3.5 “Synthesis of consumption for each mode and each module” ###
**Issue:** The power state OFF is used in the table. However, unlike ECO0/1/2 and SLEEP, this state is not defined. 

**Implementation advice:** The OFF consumption of an OFF automotive ECU is normally in the 20 – 100 uA range. Anything in that range is acceptable. The not-entirely-off value used as higher than OFF is 0.048W (2mA x 24V), so anything above 1mA would not be considered acceptable.

### Section 2.1.3.6 “ITS consumption modes compare to vehicle use phases” ###
**Issue:** Several of the vehicle use phases includes speed/movement as part of definition. Yet it is not trivial for a module to get hold of speed/movement information. Nor is it entirely clear that the desired behaviour is that modules does not turn on directly after ignition but waits until the vehicle starts moving. 

**Implementation advice:** Do not use speed/movement to calculate the vehicle use phase.

### Section 2.5.5 “Awake request (optional)” ###
**Issue:** There is no defined signal level for this signal.

**Implementation advice:** Based on the other signals defined, the reasonable assumption is that 24V would be the awake request, and that the signal should be at ground level at all other times. (However, see next issue.)

### Section 2.5.5 “Awake request (optional)” ###
**Issue:** Apart from missing a definition of signal level (see previous issue), all the spec says about the awake request signal is “Signal coming from the VCG as input to vehicle to trigger power line.” So, it is difficult to know what – if anything - will happen. 

**Implementation advice:** Since it is optional one cannot rely on this being available. But even when it is available, it is difficult to know what – if anything – will happen without knowledge of a specific installation/vehicle. Recommendation would be, for now, not to rely on this function.

### Section 2.5.1 “Low Battery information (mandatory)” ###
**Issue:** When reading the section on low battery signal, the impression is given that all ITS modules will be notified of this state and can/must take appropriate action. However, the low batt signal is present in the AUX connector of which there is only one; without some very custom wiring Low Battery signal/wire would only be connected to one module. And there is no way for that one module to distribute that information to the other modules.  

**Implementation advice:** Low Battery is mandatory for ITxPT compliant vehicles. For ITS modules it will not be considered mandatory for now, and in an actual installation it may not be available even if the module supports it. 
