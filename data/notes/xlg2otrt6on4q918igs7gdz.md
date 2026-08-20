
> https://praveshkoirala.com/2023/06/13/a-non-mathematical-introduction-to-kalman-filters-for-programmers/

1. Kalman filters combine multiple noisy measurements to produce a more accurate estimate.
2. They are useful because real-life measurements are often imperfect and unreliable due to factors like sensor noise and malfunction.
3. An example is estimating the location of a ship using both its velocity and GPS sensor measurements. Both are imperfect so a Kalman filter can combine them.
4. The Kalman filter takes a weighted average of the measurements, with more weight given to the more reliable source based on its variance.
5. The code simulates 1000 passengers on a ship estimating its location using noisy velocity and sensor measurements.
6. The Kalman filter calculates the variance of the measurements to determine the trustworthiness of each source.
7. It then takes a weighted average based on the trust values to produce a combined position estimate.
8. The results show the combined estimate is better than either measurement alone, especially when one source has a glitch.
9. The Kalman filter automatically adjusts for variations and provides a reasonably reliable estimate.
