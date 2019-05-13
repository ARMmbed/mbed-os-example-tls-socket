# Testing examples

Examples are tested using tool [htrun](https://github.com/ARMmbed/mbed-os-tools/tree/master/packages/mbed-host-tests) and templated print log. 

To run the test, use following command after you build the example:
```
mbedhtrun -d D: -p COM4 -m K64F -f .\BUILD\K64F\GCC_ARM\tls-socket.bin --compare-log tests\tls-socket.log
```


More details about `htrun` are [here](https://github.com/ARMmbed/htrun#testing-mbed-os-examples).

