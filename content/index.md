# This Project

This project aims to reduce the effect of hysteresis in CERN's accelerators as part of Work Package 4 of the Efficient Particle Accelerator project.

CERN's accelerators use various types of magnet to maintain the particle beams. Currently, hysteresis mean one cannot be sure what field one will achieve if a certain current is sent to these magnets, resulting in reduced beam quality and inefficiency across the complex. This project aims to understand and predict hysteric effects and provide a means of compensation to the machine operators.

# What is Hysteresis?

When an electric current is run through a magnetic coil, a magnetic field is generated. In an ideal case, one can turn on a magnet to a certain current which will produce a certain field based on the properties of the magnet. Then one can remove the current, reducing the field back to zero. If one applies the same current again, the same field is generated.

Unfortunately, reality is not so simple. In fact, generating a field actually changes the internal state of the magnet in an unpredictable way, which means that the next time the same current is applied the field will be subtly different. The magnet field is therefore not only dependent on the presently-applied current, but also any previously-generated field; in other words, the magnet field is influenced by its earlier values (its 'history'). This 'history dependence' is called 'magnetic hysteresis' or just 'hysteresis'.


