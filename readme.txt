Hello, here is a working example for alpha version algorithm

VAWT_BiOpt_alpha_version_20260326 Executable

1. Prerequisites for Deployment 

Verify that MATLAB Runtime(R2022b) is installed.
If not, you can run the MATLAB Runtime installer.
To find its location, enter
  
    >>mcrinstaller
      
at the MATLAB prompt.
NOTE: You will need administrator rights to run the MATLAB Runtime installer. 

Alternatively, download and install the Windows version of the MATLAB Runtime for R2022b 
from the following link on the MathWorks website:

    https://www.mathworks.com/products/compiler/mcr/index.html
   
For more information about the MATLAB Runtime and the MATLAB Runtime installer, see 
"Distribute Applications" in the MATLAB Compiler documentation  
in the MathWorks Documentation Center.

2. Files to Deploy and Package

Files to Package for Standalone 
================================
-VAWT_BiOpt_alpha_version_20260326.exe
-MCRInstaller.exe 
    Note: if end users are unable to download the MATLAB Runtime using the
    instructions in the previous section, include it when building your 
    component by clicking the "Runtime included in package" link in the
    Deployment Tool.
-This readme file 



3. Definitions

For information on deployment terminology, go to
https://www.mathworks.com/help and select MATLAB Compiler >
Getting Started > About Application Deployment >
Deployment Product Terms in the MathWorks Documentation
Center.



3. Algorithm example description

This algorithm consists of three main components: experimental data acquisition and preprocessing, algorithm training, and conclusion validation. Its primary objective is to predict the operating conditions of triple-row bio-inspired covert configurations—which yield superior flow control performance—using experimental data from single-row configurations under fewer conditions. This approach reduces the number of experiments required for triple-row configurations, allowing validation to be performed on only a few optimal cases, thereby significantly shortening the design cycle. Taking six different positions of single-row bio-inspired covert structures as an example, an exhaustive experimental investigation of all possible triple-row combinations would result in 20 distinct cases, making it impractical to conduct flow field and force measurements for each. The present example focuses on the second component—the algorithm training part—for the following reasons:

Experimental data acquisition and preprocessing are primarily based on the definition and classification of covert aerodynamic modes established in the main text. The core lies in the fluid–structure interaction mechanism of the bio-inspired covert structures, which can be characterized by the shear layer thickness and turbulence intensity in the blade wake. Since the number of single-row covert cases is limited (six in total), flow field experiments can be conducted for each case, with repeated measurements performed to ensure data adequacy. Furthermore, during data acquisition, based on observations of the kinematic behavior of the bio-inspired covert structures and in conjunction with low-order flow statistics (such as threshold values of mean velocity and turbulence intensity) that can be rapidly obtained, different control modes can be distinguished and preprocessed for grouping. This approach effectively mitigates issues such as data leakage. Experimental data exhibiting significant deviations are discarded immediately after acquisition and are not used in subsequent algorithm training.

In the conclusion validation stage, the optimal modal combination cases are obtained based on the qualitative conclusions derived from algorithm training. Comparative experiments between the optimized bio-inspired blade configurations and a clean blade configuration can validate these qualitative conclusions. Notably, to reduce measurement workload and post-processing costs, flow field sampling is not required; instead, only the mechanical performance of the blade needs to be measured to verify the optimization effect. For the predicted advantageous cases, repeated experiments are conducted to obtain a sufficiently large dataset for ablation studies. In practice, even when the probability of mutation operators in the genetic algorithm is increased, similar prediction results are achieved after sufficient iteration steps. Moreover, the proposed method integrates bio-inspired design with an experimental data-driven genetic algorithm to identify and obtain key advantageous experimental conditions; therefore, no relevant bio-inspired blade dataset is available for comparison. Additionally, owing to the uniqueness of the bio-inspired design in this study, no publicly recognized benchmark data exist within the research community.

The present example aims to fuse flow field data obtained under single-row bio-inspired covert control. Low-order flow field data (mean velocity, turbulence intensity) are rapidly utilized for data grouping during the preprocessing stage following data acquisition, while the algorithm training primarily employs the time–frequency domain distribution features obtained via wavelet decomposition of the experimental data. The physical interpretation of these features is the amplitude modulation effect of large-scale fluctuations on small-scale fluctuations, which is further used to predict flow field signals under combined multi-row bio-inspired covert control. The overarching goal of this study is to identify qualitative optimal modes and reveal deeper physical mechanisms within the flow field, rather than to achieve precise quantitative predictions. Accordingly, this paper focuses on the qualitative relationships between the kinematic modes of bio-inspired covert structures and the resulting flow structures, as well as their coupling with the mechanical properties of the blade. The primary purpose of this example is to propose this training framework and to determine the priority of synergistic modes among multi-row bio-inspired covert structures. It is worth noting that prediction accuracy can be progressively improved by increasing data input, enriching the physical features used as feedback, increasing the number and precision of genetic factors, and extending iteration steps. However, such improvements would require additional experimental cases and their repetitions, more validation experiments with flow field and force measurements, and a substantial number of cases for algorithm training. As this is not the focus of the present study, these aspects are not further elaborated.

The specific parameters of this example are described as follows:

4.1. Three sets of flow field data that have undergone preprocessing and modal classification—designated xxx1, xxx2, and xxx3—are imported for demonstration. These data correspond to velocity signals captured by a hot-wire anemometer at the trailing edge position x/c = 0.7 (where c is the blade chord length and x is the streamwise coordinate) under a critical angle of attack of 15° for a single blade, with the 20%c, 40%c, and 60%c bio-inspired covert structures acting individually. For each case, 20 measurement points are included, with a sampling frequency of 4000 Hz and 262,144 sampling points per point.

4.2. The present example focuses on time–frequency analysis based on wavelet transform. The velocity signal at each measurement point is decomposed and reconstructed into time-fluctuating signals across 16 distinct frequency scales. Through energy analysis, small-scale and large-scale signals are distinguished. Based on Hilbert decomposition, the amplitude modulation effect of large-scale fluctuations on small-scale fluctuations is analyzed. Depending on the correlation level, a new fused small-scale signal is reconstructed from the large-scale fluctuation signals of the three cases, followed by signal reconstruction. This procedure employs a genetic DNA operator, including genetic, crossover, and mutation operators, to avoid entrapment in local optima. Through iteration, the energy deviation and the correlation deviation of amplitude modulation are progressively minimized.

4.3. Two critical parameters are the number of genes and the number of iteration steps; larger values yield more accurate predictions. The original parameter settings in this study were 80 genes and 800 iteration steps, which would require substantial memory, high CPU usage, and weeks of computation time. Since this example is intended solely for demonstration purposes, with only three experimental cases available, the number of genes is set to 50 and the number of iteration steps to 200. Although the convergence performance is somewhat reduced, the resulting predictions still reasonably reflect the velocity signal xxx4 under the combined action of the 20%c, 40%c, and 60%c bio-inspired covert structures.


Copyright @XuAn Gong
2026, 03, 26


