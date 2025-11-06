# Score: 88.0/100.0

## [Pass] 1) Client and Server Compile (4/4)

### Compilation Status

This section tests if your implementation compiles with our test apparatus.

We are not looking for compilation warnings. As long as your implementation compiles in our setup, you will receive full points for this section.

Outputs from the `make` command:

```
make -C udt4 all
make[1]: Entering directory '/cs3251/student/student-src/udt4'
make[1]: Nothing to be done for 'all'.
make[1]: Leaving directory '/cs3251/student/student-src/udt4'
make -C tests all
make[1]: Entering directory '/cs3251/student/student-src/tests'
g++ -Wall -DLINUX -I../src -I../udt4 -finline-functions -g  appserver.cpp -c
g++ appserver.o -o appserver -L../udt4 -ludt -lstdc++ -lpthread -lm
g++ -Wall -DLINUX -I../src -I../udt4 -finline-functions -g  appclient.cpp -c
g++ appclient.o -o appclient -L../udt4 -ludt -lstdc++ -lpthread -lm
make[1]: Leaving directory '/cs3251/student/student-src/tests'
```

### Summary

The `make` command terminated without error. Compilation with your submission produced the expected binaries

## [Pass] 2.1) Test Server Runs (0.5/0.5)

### Server Process Output

```
server is ready at port: 9000
new connection: 127.0.0.1:58821
```

Note: it's absolutely fine if the server terminates with "recv:Connection was broken."

## [Pass] 2.2) Test Client Runs (0.5/0.5)

### Client Process Output

```
┌─────────────────┬────────────┬────────┬─────────────┐
│ SendRate (Mb/s) │  RTT (ms)  │  CWnd  │ PktInFlight │
├─────────────────┼────────────┼────────┼─────────────┤
│           0.119 │   1000.000 │      5 │           5 │
│           0.163 │    767.595 │      7 │           7 │
│           0.233 │    499.170 │      9 │           9 │
│           0.326 │    410.043 │     12 │          12 │
│           0.326 │    405.222 │     14 │          14 │
│           0.536 │    403.776 │     16 │          16 │
│           0.691 │    404.575 │     19 │          19 │
│           0.489 │    426.110 │     21 │          21 │
│           0.512 │    451.076 │     22 │          22 │
│           4.619 │    462.980 │     22 │          22 │
│           0.559 │    465.920 │     22 │          22 │
│           0.559 │    465.636 │     22 │          22 │
│           1.016 │    463.612 │     22 │          22 │
│           0.559 │    465.164 │     22 │          22 │
│           0.512 │    465.707 │     22 │          22 │
│           0.522 │    463.411 │     22 │          22 │
│           0.512 │    465.902 │     22 │          22 │
│           0.512 │    465.424 │     22 │          22 │
│           0.048 │    463.167 │     22 │          22 │
│           0.512 │    465.895 │     22 │          22 │
│           0.559 │    465.615 │     22 │          22 │
│           1.191 │    463.517 │     22 │          22 │
│           0.559 │    465.169 │     22 │          22 │
│           0.559 │    465.712 │     22 │          22 │
│           0.828 │    463.921 │     22 │          22 │
│           0.512 │    465.330 │     22 │          22 │
│           0.512 │    465.600 │     22 │          22 │
│           0.250 │    463.174 │     22 │          22 │
│           0.512 │    465.956 │     22 │          22 │
│           0.512 │    465.307 │     22 │          22 │
│           2.636 │    463.381 │     22 │          22 │
│           0.559 │    465.360 │     22 │          22 │
│           0.536 │    465.745 │     22 │          22 │
│           0.950 │    464.067 │     22 │          22 │
│           0.536 │    464.659 │     22 │          22 │
│           0.512 │    465.746 │     22 │          22 │
│           0.522 │    463.660 │     22 │          22 │
│           0.512 │    465.683 │     22 │          22 │
│           0.512 │    465.554 │     22 │          22 │
│           0.122 │    463.101 │     22 │          22 │
│           0.675 │    465.533 │     22 │          22 │
│           0.559 │    465.740 │     22 │          22 │
│           1.285 │    463.887 │     22 │          22 │
│           0.559 │    464.648 │     22 │          22 │
│           0.559 │    465.835 │     22 │          22 │
│           0.765 │    464.184 │     22 │          22 │
│           0.512 │    465.006 │     22 │          22 │
│           0.512 │    465.708 │     22 │          22 │
│           0.337 │    463.393 │     22 │          22 │
│           0.512 │    465.855 │     22 │          22 │
│           0.629 │    465.665 │     22 │          22 │
│           0.410 │    463.962 │     22 │          22 │
│           0.559 │    464.811 │     22 │          22 │
│           0.559 │    465.833 │     22 │          22 │
│           1.057 │    464.605 │     22 │          22 │
│           0.512 │    464.329 │     22 │          22 │
│           0.512 │    465.772 │     22 │          22 │
│           0.521 │    463.887 │     22 │          22 │
│           0.512 │    465.311 │     22 │          22 │
│           0.512 │    465.646 │     22 │          22 │
│           0.211 │    463.138 │     22 │          22 │
└─────────────────┴────────────┴────────┴─────────────┘

Summary of the last 45 seconds:
* Average Rate: 0.611
* Average CWnd: 22.000
* RTT Std Dev:  0.954
```

## [Pass] 2.3) Measured RTT Standard Deviation (7/7)

Testing your implementation with a queue limit of 10000 packets and a delay of 200.00 ms. A lower standard deviation indicates that your implementation is more stable at transmitting data.

- Your implementation should have a sustained RTTStdDev of 5.00 ms or less to receive full points.
- Your measured RTTStdDev in this scenario was 0.95 ms

## [Pass] 2.4) Measured Throughput (24/24)

Testing your implementation with line rate limited to 1.00 Mbps. A higher throughput indicates that your implementation is more efficient at utilizing the available bandwidth.

- Your implementation should reach at least 0.20 Mbps to receive partial points and 0.40 Mbps to receive full points.
- Your measured throughput in this scenario was 0.61 Mbps

## [Pass] 3.1) Test Server Runs (0.5/0.5)

### Server Process Output

```
server is ready at port: 9000
new connection: 127.0.0.1:57438
```

Note: it's absolutely fine if the server terminates with "recv:Connection was broken."

## [Pass] 3.2) Test Client Runs (0.5/0.5)

### Client Process Output

```
┌─────────────────┬────────────┬────────┬─────────────┐
│ SendRate (Mb/s) │  RTT (ms)  │  CWnd  │ PktInFlight │
├─────────────────┼────────────┼────────┼─────────────┤
│           0.024 │   1000.000 │      5 │           5 │
│           0.233 │    927.603 │      7 │           7 │
│           0.210 │    760.923 │      9 │           9 │
│           0.256 │    617.884 │     11 │          11 │
│           0.303 │    524.337 │     13 │          13 │
│           0.396 │    455.686 │     15 │          15 │
│           0.466 │    419.432 │     17 │          17 │
│           0.449 │    406.076 │     19 │          19 │
│           0.629 │    401.472 │     21 │          21 │
│           0.536 │    400.562 │     23 │          23 │
│           0.885 │    400.550 │     26 │          26 │
│           0.887 │    400.390 │     28 │          28 │
│           0.722 │    401.584 │     30 │          30 │
│           0.949 │    401.039 │     32 │          32 │
│           0.758 │    400.833 │     34 │          34 │
│           1.391 │    400.580 │     37 │          37 │
│           1.092 │    400.757 │     39 │          39 │
│           0.955 │    400.558 │     41 │          41 │
│           0.585 │    400.826 │     43 │          43 │
│           1.071 │    400.488 │     46 │          46 │
│           0.501 │    400.835 │     48 │          48 │
│           0.268 │    400.443 │     50 │          50 │
│           1.547 │    401.011 │     53 │          53 │
│           1.544 │    401.247 │     55 │          55 │
│           1.664 │    401.030 │     57 │          57 │
│           1.658 │    401.213 │     60 │          60 │
│           1.956 │    401.128 │     62 │          62 │
│           2.323 │    400.849 │     65 │          65 │
│           1.819 │    400.761 │     67 │          67 │
│           1.940 │    401.428 │     69 │          69 │
│           1.850 │    400.735 │     72 │          72 │
│           1.363 │    400.326 │     74 │          74 │
│           2.101 │    400.656 │     76 │          76 │
│           4.476 │    400.410 │     79 │          79 │
│           5.323 │    400.746 │     81 │          81 │
│           4.106 │    400.977 │     84 │          84 │
│           2.557 │    400.813 │     86 │          86 │
│           7.678 │    401.459 │     88 │          88 │
│           2.623 │    400.625 │     90 │          90 │
│           9.457 │    400.651 │     93 │          93 │
│           2.133 │    400.402 │     95 │          95 │
│           2.655 │    402.404 │     98 │          98 │
│           1.067 │    401.568 │    100 │         100 │
│           5.278 │    400.877 │    102 │         102 │
│           3.955 │    400.451 │    105 │         105 │
│           2.052 │    401.017 │    107 │         107 │
│           4.181 │    400.596 │    110 │         110 │
│           8.050 │    401.288 │    112 │         112 │
│           3.890 │    401.151 │    114 │         114 │
│           3.660 │    401.539 │    117 │         117 │
│           4.909 │    400.962 │    119 │         119 │
│           4.801 │    401.568 │    121 │         121 │
│           5.168 │    401.537 │    124 │         124 │
│           2.674 │    401.894 │    126 │         126 │
│           5.572 │    401.537 │    129 │         129 │
│           2.678 │    402.291 │    131 │         131 │
│           5.003 │    401.770 │    133 │         133 │
│           2.860 │    402.398 │    136 │         136 │
│           7.920 │    401.622 │    138 │         138 │
│           2.728 │    400.653 │    140 │         140 │
│           6.815 │    400.945 │    143 │         143 │
└─────────────────┴────────────┴────────┴─────────────┘

Summary of the last 45 seconds:
* Average Rate: 3.368
* Average CWnd: 91.222
* RTT Std Dev:  0.503
```

## [Pass] 3.3) Measured RTT Standard Deviation (7/7)

Testing your implementation with a queue limit of 10000 packets and a delay of 200.00 ms. A lower standard deviation indicates that your implementation is more stable at transmitting data.

- Your implementation should have a sustained RTTStdDev of 10.00 ms or less to receive full points.
- Your measured RTTStdDev in this scenario was 0.50 ms

## [Pass] 3.4) Measured Throughput (24/24)

Testing your implementation with line rate limited to 10.00 Mbps. A higher throughput indicates that your implementation is more efficient at utilizing the available bandwidth.

- Your implementation should reach at least 2.00 Mbps to receive partial points and 3.00 Mbps to receive full points.
- Your measured throughput in this scenario was 3.37 Mbps

## [Pass] 4.1) Test Server Runs (0.5/0.5)

### Server Process Output

```
server is ready at port: 9000
new connection: 127.0.0.1:54534
```

Note: it's absolutely fine if the server terminates with "recv:Connection was broken."

## [Pass] 4.2) Test Client Runs (0.5/0.5)

### Client Process Output

```
┌─────────────────┬────────────┬────────┬─────────────┐
│ SendRate (Mb/s) │  RTT (ms)  │  CWnd  │ PktInFlight │
├─────────────────┼────────────┼────────┼─────────────┤
│           0.000 │   1000.000 │      5 │           5 │
│           0.140 │    982.827 │      6 │           6 │
│           0.163 │    937.105 │      7 │           7 │
│           0.163 │    844.408 │      9 │           9 │
│           0.233 │    777.520 │     10 │          10 │
│           0.140 │    723.544 │     11 │          11 │
│           0.303 │    669.310 │     13 │          13 │
│           0.912 │    642.085 │     15 │          15 │
│           0.163 │    623.347 │     16 │          16 │
│           0.303 │    611.500 │     17 │          17 │
│           0.233 │    605.127 │     19 │          19 │
│           0.303 │    602.513 │     20 │          20 │
│           0.276 │    601.216 │     22 │          22 │
│           0.489 │    600.774 │     23 │          23 │
│           0.540 │    600.465 │     25 │          25 │
│           0.559 │    600.348 │     26 │          26 │
│           0.696 │    600.405 │     28 │          27 │
│           0.210 │    600.866 │     29 │          29 │
│           0.703 │    600.611 │     31 │          31 │
│           2.098 │    600.412 │     32 │          32 │
│           0.582 │    600.571 │     34 │          34 │
│           0.582 │    600.522 │     35 │          35 │
│           1.289 │    600.543 │     37 │          37 │
│           0.373 │    600.516 │     38 │          38 │
│           0.745 │    600.343 │     40 │          40 │
│           0.699 │    600.664 │     41 │          41 │
│           0.606 │    600.484 │     43 │          43 │
│           0.932 │    600.290 │     44 │          44 │
│           0.838 │    600.256 │     46 │          46 │
│           0.606 │    600.276 │     47 │          47 │
│           0.978 │    600.292 │     49 │          49 │
│           0.641 │    600.292 │     50 │          50 │
│           0.559 │    600.416 │     52 │          52 │
│           0.642 │    600.916 │     53 │          53 │
│           1.479 │    600.594 │     55 │          55 │
│           0.722 │    600.520 │     56 │          56 │
│           0.813 │    600.438 │     58 │          58 │
│           1.365 │    600.402 │     60 │          60 │
│           0.838 │    600.563 │     61 │          61 │
│           1.099 │    600.771 │     63 │          63 │
│           0.932 │    600.745 │     64 │          64 │
│           0.473 │    600.628 │     66 │          66 │
│           2.084 │    600.864 │     68 │          68 │
│           4.415 │    600.502 │     69 │          69 │
│           1.324 │    600.717 │     71 │          71 │
│           2.573 │    600.639 │     73 │          73 │
│           4.921 │    600.917 │     74 │          74 │
│           1.657 │    600.535 │     76 │          76 │
│           2.257 │    600.674 │     77 │          77 │
│           1.514 │    600.354 │     79 │          79 │
│           0.751 │    600.429 │     80 │          80 │
│           1.636 │    600.733 │     82 │          82 │
│          11.774 │    601.078 │     84 │          84 │
│           1.614 │    600.632 │     85 │          85 │
│           1.904 │    600.715 │     87 │          87 │
│           1.118 │    600.635 │     88 │          88 │
│           1.881 │    600.486 │     90 │          90 │
│           2.604 │    600.498 │     92 │          92 │
│           1.211 │    600.747 │     93 │          93 │
│           1.443 │    600.875 │     95 │          95 │
│           4.187 │    600.715 │     96 │          96 │
└─────────────────┴────────────┴────────┴─────────────┘

Summary of the last 45 seconds:
* Average Rate: 2.229
* Average CWnd: 61.944
* RTT Std Dev:  0.192
```

### [Pass] 4.3) Measured RTT Standard Deviation (7/7)

Testing your implementation with a queue limit of 10000 packets and a delay of 300.00 ms. A lower standard deviation indicates that your implementation is more stable at transmitting data.

- Your implementation should have a sustained RTTStdDev of 30.00 ms or less to receive full points.
- Your measured RTTStdDev in this scenario was 0.19 ms

### 4.4) [Fail] Measured Throughput (12/24)

Testing your implementation with line rate limited to 10.00 Mbps. A higher throughput indicates that your implementation is more efficient at utilizing the available bandwidth.

- Your implementation should reach at least 2.00 Mbps to receive partial points and 3.00 Mbps to receive full points.
- Your measured throughput in this scenario was 2.23 Mbps