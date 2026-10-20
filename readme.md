# Delay-Phased Array (DPA) mmFlexible: A flexible frequency-division multiplexing technique for multi-user millimeter wave networks with MATLAB code

I. Summary
The modern mmWave systems have limitations in frequency reuse flexibility, which restricts their scalability. All frequency components within the signal are directed to a single direction through pencil-shaped beamforming, preventing transmission to other users' directions. To address this issue, this paper proposes a novel flexible mmWave system named mmFlexible, capable of flexible directional frequency reuse, allowing different frequency components of mmWave signals to be beamformed in multiple arbitrary directions through the same pencil-shaped beam.

The core contributions of this system include two aspects:
1. A new mmWave frontend architecture called "Delay-Phased Array" has been designed, generating the required frequency - direction response through variable delay and phased elements.
2. A new algorithm named FSDA (Frequency-space to delay-antenna) is proposed for estimating the delay and phase values required by the real-time operation of the delay-phased array.

Through mmWave channel trajectory evaluations, it has been shown that compared to the baseline system, mmFlexible can reduce the worst-case delay by 60%-150%.

II. Introduction
MmWave networks possess vast bandwidth resources, offering potential for providing wireless connectivity to an increasing number of users. However, current mmWave systems face significant limitations: they cannot allocate small frequency band resources to users in different directions simultaneously.

Unlike Sub-6 (below 6GHz) systems that use omnidirectional antennas to radiate signals in all directions, mmWave systems employ pencil-shaped beamforming, covering only a small area in space —— meaning all frequency components are directed to a fixed direction, unable to be allocated to other directions. This lack of flexibility leads to two major issues (as shown in Figure 1 (a)):
High latency: Base stations (gNBs) must serve users in different directions in a time-division manner, with some users waiting for extended periods, which is highly detrimental to delay-sensitive applications such as VR and URLLC.
2. Low effective spectral utilization: When a base station serves only one device at a time, the device receives a significant amount of instantaneous capacity, but may not fully utilize it due to its own demands; the base station cannot direct the remaining frequency resources towards other directions, leading to resource wastage, and other directions' users could have utilized these bands to enhance overall spectral utilization.
The core question proposed in this paper is: "Can millimeter wave base stations generate flexible frequency-direction beamforming responses by sending or receiving signals through any set of consecutive bands to any direction?" Although large antenna arrays and digital beamforming can achieve this goal, traditional millimeter wave systems rely on analog phased arrays with a single RF chain to accommodate cost and power efficiency, failing to generate such frequency-direction responses. If the phased array were split into multiple subarrays and directed towards different directions, it would reduce the directionality of each direction, leading to signal strength, transmission range, reliability, and even data rate degradation.
In recent years, new millimeter wave front-end architectures such as real-time delay (TTD) arrays and leaky wave antennas have been proposed, capable of achieving frequency-related beamforming and allocating different frequencies to different directions. However, these architectures have limitations: each user can only obtain a very small bandwidth within a time slot, potentially not meeting their needs; and they cannot control the number of beams, beam directions, and beam bandwidth (system bandwidth that has high shaping gain in the target direction and low gain in other directions), resulting in a significant waste of frequency resources in unactive directions, leaving spectral utilization still low.
This paper proposes the mmFlexible system, which achieves flexible directional frequency multiplexing by assigning a continuous set of frequency resources to each user (regardless of their directions), thereby avoiding spectrum wastage. The core of mmFlexible is the generation of multiple concurrent pencil beams in different user directions, with each beam carrying an independent frequency band according to the needs of users in the corresponding direction. The multi-beam response of mmFlexible can maintain shaping gain across all beams while only distributing power to target frequency - direction pairs, with minimal leakage to other directions and bands; and frequency - direction pairs can be selected at will, providing flexibility for directional frequency multiplexing. This allows the system to efficiently utilize the entire bandwidth (up to 800MHz in 5G NR and up to 2.3GHz in IEEE 802.11ax), reducing spectrum wastage and achieving low latency network access (as shown in Figure 1(b)).
To realize mmFlexible, this paper also introduces the "Delay-Phased Array (DPA)" as a new millimeter wave analog array architecture that generates versatile multi-beams in terms of number, direction, and bandwidth (as shown in Figure 2). Unlike fixed delay architectures, DPA uses variable delay and phase elements at each antenna, complementing each other's effects (the variable delay provides frequency selectivity, and the phase element provides directional control) to achieve multi-beam shaping towards any frequency - direction pair.
In hardware implementation of DPA, this paper analyzes the required delay range and resolution for generating target multi-beams and addresses the challenges of large delay circuit size and integration difficulty in millimeter wave frequencies — compared to traditional TTD arrays, DPA significantly reduces the delay range (e.g., in a 16-antenna array, TTD requires 20ns delay, which is 13 times larger than existing millimeter wave delay designs, while DPA's delay range can be adjusted alternately, making it even smaller), and the delay range is independent of the number of antennas, facilitating large-scale array expansion.
In software programming, to address the non-convex and NP-hard problem of DPA delay and phase discrete value solving (the number of combinations for all frequency - direction pairs is 10²⁸, which is completely unfeasible), this paper proposes an FSDA algorithm. It maps the target frequency - space response to delay - antenna space through a 2D transformation, extracting the delay and phase values of each antenna in real time, and can be implemented based on fast 2D FFT technology. This algorithm only requires user-angle and current time slot allocation frequency resources, while angles can be obtained through standard initial access protocols, facilitating integration with existing 5G mmWave protocols.
In summary, the core contributions of mmFlexible are summarized as follows:
1.  
It is the first system to implement flexible frequency reuse for millimeter wave networks, improving spectrum utilization, reducing latency, and supporting large user expansion.
2.  
A delay phased array (DPA) architecture is designed, maintaining high shaping gain while enabling flexible beam number, direction, and bandwidth generation.
3.  
An FSDA algorithm is proposed, based on 2D FFT to estimate delay and phase in real time, and is easy to integrate with 5G mmWave standard protocols.
4.  
Real mmWave trajectory evaluation shows that mmFlexible reduces latency by 60%-150% compared to the baseline system, and the total throughput of multiple users increases by 3.9 times compared to the TTD array baseline.
Conclusion: The mmFlexible system proposed in this paper, through the combination of "delay phased array (DPA)" hardware architecture and "FSDA" software algorithm, breaks through the flexibility bottleneck of traditional millimeter wave systems in directional frequency reuse, providing a low latency and high spectral utilization solution for multi-user millimeter wave networks.
From the hardware perspective, DPA architecture innovatively combines variable delay with variable phase elements, addressing the limitations of traditional phased arrays' "single-directional beam" and TTD arrays' "fixed frequency - direction mapping." The delay range is independent of the number of antennas, significantly reducing the difficulty of hardware implementation at millimeter wave frequencies and supporting large-scale array expansion.
From the software perspective, the FSDA algorithm transforms the complex problem of delay-phase resolution into a real-time processable flow through 2D transformation, avoiding the resource waste of brute force precomputation. It only relies on standard protocol user-angle information for obtaining, making it easy to integrate with existing 5G mmWave systems.
Performance evaluation shows that in a 10-user scenario of 4K VR, mmFlexible can control the air interface delay within 0.5ms, without packet loss, and achieve a throughput of 71.3Mbps, far exceeding traditional phased arrays (delay > 1.25ms, packet loss 24%, throughput 54.9Mbps), split antenna arrays (delay > 2ms, packet loss 33.3%, throughput 47.3Mbps), and TTD arrays (delay > 3.5ms, packet loss 76.4%, throughput 18.3Mbps). At the same time, the total throughput of multiple users is increased by 3.9 times compared to the TTD array, and the SNR ratio when angle separation is large is up to 3-5dB higher than the baseline of split antennas, fully verifying its advantages in delay-sensitive and high throughput scenarios.
In the future, the application of mmFlexible can be further expanded: on the hardware side, consider exploring implementation of mid-frequency (Sub-6GHz) delay elements to improve delay precision; on the system level, expand to multi-radio chain architecture to achieve wider flexible frequency band allocation; on the scenario side, its controllable frequency-space beam characteristics can also be used in areas such as multi-target positioning tracking, communication and perception integration, providing a foundation for diverse applications of millimeter wave technology.
End

## Images

![(Delay-Phased Array DPA)mmFlexible: Flexible Directional Frequency Reuse Technology for Multi-User Millimeter Wave Networks [with MATLAB Code]](01.jpg)
![(Delay-Phased Array DPA)mmFlexible: Flexible Directional Frequency Reuse Technology for Multi-User Millimeter Wave Networks [with MATLAB Code]](02.jpg)
![(Delay-Phased Array DPA)mmFlexible: Flexible Directional Frequency Reuse Technology for Multi-User Millimeter Wave Networks [with MATLAB Code]](03.jpg)
![(Delay-Phased Array DPA)mmFlexible: Flexible Directional Frequency Reuse Technology for Multi-User Millimeter Wave Networks [with MATLAB Code]](04.jpg)
![(Delay-Phased Array DPA)mmFlexible: Flexible Directional Frequency Reuse Technology for Multi-User Millimeter Wave Networks [with MATLAB Code]](05.jpg)
![(Delay-Phased Array DPA)mmFlexible: Flexible Directional Frequency Reuse Technology for Multi-User Millimeter Wave Networks [with MATLAB Code]](06.jpg)
![(Delay-Phased Array DPA)mmFlexible: Flexible Directional Frequency Reuse Technology for Multi-User Millimeter Wave Networks [with MATLAB Code]](07.jpg)
![(Delay-Phased Array DPA)mmFlexible: Flexible Directional Frequency Reuse Technology for Multi-User Millimeter Wave Networks [with MATLAB Code]](08.jpg)
![(Delay-Phased Array DPA)mmFlexible: Flexible Directional Frequency Reuse Technology for Multi-User Millimeter Wave Networks [with MATLAB Code]](09.jpg)
![(Delay-Phased Array DPA)mmFlexible: Flexible Directional Frequency Reuse Technology for Multi-User Millimeter Wave Networks [with MATLAB Code]](10.jpg)
![(Delay-Phased Array DPA)mmFlexible: Flexible Directional Frequency Reuse Technology for Multi-User Millimeter Wave Networks [with MATLAB Code]](11.jpg)
![(Delay-Phased Array DPA)mmFlexible: Flexible Directional Frequency Reuse Technology for Multi-User Millimeter Wave Networks [with MATLAB Code]](12.jpg)
![(Delay-Phased Array DPA)mmFlexible: Flexible Directional Frequency Reuse Technology for Multi-User Millimeter Wave Networks [with MATLAB Code]](13.jpg)

<!-- PAYMENT_BLOCK -->

## Get this dataset

- Payment link (Stripe): [Buy now](https://buy.stripe.com/3cs8yP7sY87d0vu9AB)
- Payment QR code: ![Payment QR code](pay.png)

<!-- /PAYMENT_BLOCK -->
