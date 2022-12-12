```shell
$ fname=060; mkdir /workon/jm/test/$fname; ./jmeter -n -t /workon/jm/test/mqtt_connect.jmx -l /workon/jm/test/$fname/result.jtl -e -o /workon/jm/test/$fname/output -r
```

```shell
$ outpath=001
$ mkdir /workon/jmeter/output/${outpath}
$ docker run --rm \
  -v $(pwd):/jmeter \
  runcare/jmeter-master \
  jmeter -n -e \
  -t /jmeter/MqttTest.jmx \
  -l /jmeter/output/${outpath}/result.jtl \
  -j /jmeter/output/${outpath}/result.log \
  -o /jmeter/output/${outpath}/  \
  -R 172.17.0.4
```

```shell
$ docker run -d -ti --name=jmm -v $(pwd):/jmeter  runcare/jmeter-master
```

