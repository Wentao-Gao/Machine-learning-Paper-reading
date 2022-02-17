# EA-DFPSO: An intelligent energy-efficient scheduling algorithm for mobile edge networks(EA-DFPSO：移动边缘网络的智能节能调度算法)



## Abstract

由于移动终端的计算能力有限，云数据中心已经被数据密集型应用程序淹没。[移动边缘计算](https://www.sciencedirect.com/topics/engineering/mobile-edge-computing)正在成为一种潜在的范式，可以在网络边缘托管应用程序执行以减少传输延迟。计算节点通常分布在边缘环境中，从而在这些节点之间实现至关重要的高效任务调度，以减少处理时间。此外，必须节省边缘服务器的能源，延长其使用寿命。

为此，本文提出了一种新的任务调度算法——Energy-aware Double-fitness [Particle Swarm Optimization](https://www.sciencedirect.com/topics/engineering/particle-swarm-optimization)(EA-DFPSO)，它基于改进的粒子群优化算法，用于在边缘计算环境中实现能源效率以及最短的任务执行时间。所提出的 EA-DFPSO 算法应用双重适应度函数来搜索最佳任务调度方案，以节省边缘服务器的能量，同时保持任务的服务质量。大量实验表明，我们提出的 EA-DFPSO 算法在减少任务完成时间和在边缘计算环境中节约能源方面优于现有的传统调度算法。



## 1. Introduction

[物联网](https://www.sciencedirect.com/topics/engineering/internet-of-things)(IoT) 设备和移动终端的最新发展，以及第五代 (5G) 通信技术的演进，带来了前所未有的数据量。

但它们在电池容量和计算能力方面的限制限制了它们承载涉及大量数据处理的重量级计算应用程序的能力，此外，延迟和延迟敏感的应用程序需要立即处理数据，因此此类应用程序中发生的任何不良延迟都可能很容易影响用户体验。

因此，从用户体验的角度来看，协调移动设备和后端服务器的计算能力可以帮助进行密集的数据处理，而不会产生不必要的延迟。

企业和个人客户越来越多地使用云计算来托管密集的数据处理应用程序，由于从终端设备向云数据中心传输大量数据而导致的网络拥塞，需要制定战略方法来缓解这一问题。

边缘计算是最近出现的一种计算范式，它将后端计算节点扩展到网络边缘 。[与传统的云架构相比，边缘计算将边缘节点放置在更靠近终端设备的物理位置，利用这些节点可以大大减少网络传输](https://www.sciencedirect.com/topics/engineering/electric-power-transmission-networks)带来的时延.

边缘计算不能被视为云计算的替代品，而是可以与云架构结合使用，以提升整个网络的功能效率，如图[1所示](https://www.sciencedirect.com/science/article/pii/S2352864821000717#fig1)。

然而，许多边缘设备具有计算能力和电源限制的特点。

为此，本文提出了一种新的任务调度算法，命名为 Energy-aware Double-fit-fit [Particle Swarm Optimization](https://www.sciencedirect.com/topics/engineering/particle-swarm-optimization)(EA-DFPSO)，它基于改进的粒子群优化 (PSO) 算法，用于在边缘计算环境中实现能源效率。我们提出的调度算法利用优化的惯性权重来帮助 EA-DFPSO，同时实现全局最佳解决方案。

本文的重要贡献包括：

- 1) 设计了用于节能调度的双重适应度函数并将其植入到 PSO 算法中，并仔细考虑了边缘服务器节点的任务完成时间和能耗。

- 2) 我们提出的新型调度算法中使用了优化的惯性权重，这有助于我们提出的启发式算法实现全局最佳解决方案。

- 3) 为边缘任务开发了一种名为 EA-DFPSO 的能量感知调度算法，以降低边缘节点的能耗，同时确保任务成功完成。

  

  

  ![图。1](https://ars.els-cdn.com/content/image/1-s2.0-S2352864821000717-gr1.jpg)

## 2. Related Work

多年来，将应用程序从用户设备卸载到边缘设备一直是热门研究焦点。

最近的几项研究从不同的角度研究了边缘计算的节能方案。

提出了一种具有动态电压频率支持（DVFS）技术的用户满意度感知能源管理模型,收集上一个周期的用户反馈，以提高当前实例的用户满意度。

提出了一种最大缓存值 (MCV) 策略来管理边缘计算设备中的缓存。

提出了一种能量感知数据传输的[路由算法](https://www.sciencedirect.com/topics/engineering/routing-algorithm)[[ 22](https://www.sciencedirect.com/science/article/pii/S2352864821000717#bib22) ]，首先根据属性和优先级对数据进行分类，确保最重要的数据可以优先传输到适当的计算节点。

另一项研究制定了一个公平的体验质量 (QoE) 和能量联合优化问题。

基于博弈论提出了一种任务分配框架[ [24 \]，以克服社交感知应用程序的延迟敏感性问题。](https://www.sciencedirect.com/science/article/pii/S2352864821000717#bib24)

为了降低边缘计算的能耗，提出了虚拟机（VM）迁移和能量调度的系统模型[ [25](https://www.sciencedirect.com/science/article/pii/S2352864821000717#bib25) ]，综合考虑任务分配、服务迁移和能量调度，以降低整体能耗。

提出了一种离散调度优化模型，证明了该问题难度的非确定性多项式（NP）性质。

提出了一种在线和[多项式时间](https://www.sciencedirect.com/topics/engineering/polynomial-time)复杂度模型[ [26 ](https://www.sciencedirect.com/science/article/pii/S2352864821000717#bib26)]，即节能动态卸载算法（EEDOA），用于解决[MEC中的泛洪问题](https://www.sciencedirect.com/topics/engineering/mobile-edge-computing)以最小化能耗，并克服[物联网的延迟性能问题](https://www.sciencedirect.com/topics/engineering/internet-of-things)设备。

## 3. Math formulas

[本节描述了我们提出的基于 PSO 的元启发式任务调度算法，用于在移动边缘计算](https://www.sciencedirect.com/topics/engineering/mobile-edge-computing)环境中实现能源效率。

#### 3.1. 介绍了PSO算法数学模型

#### 3.2 . 具有惯性权重的改进 PSO

#### 3.3. MEC 中的工作负载调度

 我们研究的最终目标是找到最优的任务分配方案，从而将执行持续时间和能耗保持在尽可能低的水平。

![图 2](https://ars.els-cdn.com/content/image/1-s2.0-S2352864821000717-gr2.jpg)

#### 3.4 . 问题编码

 在 PSO 算法中，粒子编码方法通常可以分为直接编码和间接编码。我们在本文中提出的改进 PSO 算法使用间接编码对粒子进行编码。

#### 3.5. 粒子群初始化

#### 3.6. 能耗模型

 当任务在物理节点上运行时，能耗主要包括处理器的计算能力和数据传输能力。

在我们的调度方案中，每个粒子都代表一个可行的调度方案，这使得粒子质量评估至关重要。

PSO 算法的适应度函数通常是唯一的，针对不同的问题呈现不同的值。

#### 3.7. 粒子属性设置

在粒子群优化中，每个粒子都有两个基本属性：位置和速度。粒子的位置表示粒子与目标之间的距离关系。速度表示粒子运动的方向和速度。

粒子不断更新其粒子速度和位置。同时不断更新粒子的局部最优位置和全局最优位置。<mark>这个更新过程的方向总是朝着全局最优解前进，并且更新一直持续到找到最终的全局最优解或者达到迭代次数的上限为止。</mark>此时，系统的解被认为是最优解。

#### 3.8 . EA-DFPSO算法说明

为了更好地理解我们提出的 EA-DFPSO 算法在边缘环境中的执行以提高能效，[算法 1](https://www.sciencedirect.com/science/article/pii/S2352864821000717#enun_Algorithm_1)详细描述了粒子选择过程。所提出的调度算法使用适应度函数来[减少能量消耗](https://www.sciencedirect.com/topics/engineering/reducing-energy-consumption)，同时完成所有任务



<img src="https://ars.els-cdn.com/content/image/1-s2.0-S2352864821000717-fx1_lrg.jpg" alt="img" style="zoom:30%;" />

## 4. Experiment

#### 4.1 实验设置

硬件环境：[CPU](https://www.sciencedirect.com/topics/engineering/central-processing-unit) - Intel Core i7-8550U @1.8Hz，8G 内存，仿真过程主要在 Cloudsim 4.0上进行

#### 4.2 基准

###### 4.2.1 . 短期工作优先 (SJF)

SJF调度算法优先考虑短作业

###### 4.2.2 . 先到先服务 (FCFS)  

任务是根据它们到达队列的顺序来调度的

###### 4.2.3 . 循环赛

Round Robin算法通过在执行下一个任务之前指定每个任务执行的时间长度，为调度程序设置一个固定的时隙。



## 5. Experiment performance evaluation

#### 5.1. 评估不同数量任务的执行时间

进行了初始评估以评估包含不同数量任务的一系列作业的执行时间，此外，还探讨了包含固定数量的 VM 的任务数量对完成时间的影响。

#### 5.2 . 在不同数量的虚拟机上评估任务执行时间

本节评估我们提出的 EA-DFPSO 调度算法相对于传统调度算法对具有不同 VM 数量的固定数量任务的性能。

#### 5.3 . 能耗评估

本节评估我们提出的 EA-DFPSO 算法在边缘环境中与其他三种调度算法的能量性能。



## 6. Conclusion

边缘计算被证明是这种对延迟敏感的应用程序的有前途的解决方案，在边缘托管任务执行。但是，边缘计算还需要优化的调度策略来在边缘节点之间分配任务，以实现更快的完成和节能。

本文基于改进的 PSO 算法，提出了一种新的任务调度算法，用于在边缘计算环境中实现能源效率，称为 EA-DFPSO。所提出的算法应用双重适应度函数来搜索优化的任务调度方案，以节省边缘服务器的能源。同时，在我们提出的调度算法中使用了优化的惯性权重，这有助于 EA-DFPSO 实现最佳性能。

我们计划开发一种新颖的节能调度模型，在我们未来的工作中协作和协调云和边缘计算之间的任务执行。