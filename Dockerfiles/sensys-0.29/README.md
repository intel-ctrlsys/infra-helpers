## Sensys 0.29

This is image is intended to be used as a first try of sensys with the need of installation. Notice that this image has not beed tested in deep, it might have issues.

To pull this image run:

```
docker pull intelctrlsys/sensys-0.29
```

To run, for example, the coretemp sensor with a sample rate of 5 seconds:

```
docker run -ti intelctrlsys/sensys-0.29 /opt/sensys/bin/orcmd --omca sensor heartbeat,coretemp --omca sensor_base_sample_rate 5
```

Also, the `orcmsched` program can be launched with:

```
docker run -ti intelctrlsys/sensys-0.29 /opt/sensys/bin/orcmsched
```

