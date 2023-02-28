# SnuQuant: Qhack-2023
# Quantum ensemble learning for classification with various quantum classifiers
<img width="1010" alt="img" src="https://user-images.githubusercontent.com/87353188/221876124-424fcc0b-51d3-4c73-97cc-144e6731f2ab.png">
Ensemble learning is a technique where multiple machine learning models are combined to improve the overall performance of the system. In quantum machine learning, ensemble learning can also be used to improve classification accuracy by combining the outputs of multiple quantum algorithms.<br/>
Therefore, Our goal is to put together various quantum algorithms such as Quantum Support Vector Machine(QSVM), Variational Quantum Classifier(VQC), Data re-uploading method into ensemble learning for classification so that we can utilise quantum advantages from each methods.<br/>
Also, we used different hardware based simulators such as Ion trap, Superconducting qubit from IonQ, Ibm Quantum to test hardware capabilities.
Different hardware platforms have different strengths and limitations. For example, superconducting qubits can typically achieve higher gate fidelities than ion traps, but ion traps have better connectivity between qubits. QSVM, VQC both have many gates and controlled operations so those are adequate algorithms to test capabilities of Ion trap Superconducting qubit.<br/>

# Quantum Support Vector Machine
<img width="609" alt="img2" src="https://user-images.githubusercontent.com/87353188/221887098-136e5ab2-ecdd-4dc2-a1fe-b387eb6e3b6c.png"><br/>
__[from Supervised learning with quantum-enhanced feature spaces]__<br/>
Simply we can obtain Quantum kernel from quantum circuit like above and just run svm algorithm to get classification. Also, we can implement QSVM with quantum annealing method using D-wave, but in this project we didn't use that method.<br/>
After trying different feature_maps such as ZZfeature_map, Zfeature_map, PauliFeature_map, StatePreparation method, and we chose ZZfeature_map.
We implemented on statevector simulator, Aersimulator from ibm_sherbrooke machine, Ionq_simulator. Also, for error correction, we applied Dynamical Decoupling sequence into feature_map circuit like below.
![output](https://user-images.githubusercontent.com/87353188/221882829-9e50ec58-9f3d-4ca3-9942-62b219229b0d.png)<br/>

# Variational Quantum Classifier
<img width="564" alt="img3" src="https://user-images.githubusercontent.com/87353188/221881923-418fe04c-de4f-4e6c-9d89-efeb863e6d19.png">
Encoding input data into quantum circuit using feature_map and apply variational circuit called W. Then, after repeated sequences of getting measurement, optimizing the parameters... We can get classification result.<br/>
So after trying different feature_maps, Ansatzs, we chose ZZfeature_map and RealAmplitude ansatz.<br/> We can modified those feature_maps, ansatz using knitting tools(https://github.com/Qiskit-Extensions/circuit-knitting-toolbox) but in this project, we used simple circuits from Qiskit.circuit.library(https://qiskit.org/documentation/apidoc/circuit_library.html)<br/>
We implemented on statevector simulator, Aersimulator from ibm_sherbrooke machine, Ionq_simulator. Also, for error correction, we applied Dynamical Decoupling sequence into feature_map circuit as same as QSVM.<br/>

# Data re-uploading classifier

<img width="925" alt="img4" src="https://user-images.githubusercontent.com/87353188/221885745-16dd6bc0-655d-4c43-aa48-2e4794c09b82.png">
<img width="406" alt="img5" src="https://user-images.githubusercontent.com/87353188/221887950-06ba2189-3bf8-484c-98af-235b14ea24b3.png">

In data re-uploading method, there are series of data encoding and single qubit operations based on universality of arbitrary single qubit rotation.
Also, we can use multiple qubits as well, but in this project we only used single qubit as a classifier.<br/>

<img width="645" alt="img6" src="https://user-images.githubusercontent.com/87353188/221888637-dc66df49-ddcc-4713-953a-1c0746ccb6d9.png">

Also, we did simple modification on this compact encoding scheme a little bit to reduce circuit depth.<br/>
Since, this circuit is composed of series of U = RZRYRZ gate,<br/>
for example, if # of layers are 2, we can reduce circuit depth like  RZRY RZRZ RYRZ -> RZRY RZ RYRZ.<br/>
So original circuit depth was 3 * # of layers, we reduced this depth into 2* # of layers + 1. Therfore, we can get more compact circuit.<br/>

# Dataset
We used Haberman's survival dataset(https://archive.ics.uci.edu/ml/datasets/haberman's+survival)
Features
1. Age of patient at time of operation (numerical)<br/>
2. Patient's year of operation (year - 1900, numerical)<br/>
3. Number of positive axillary nodes detected (numerical)<br/>

Class : Survival status <br/>
1 = the patient survived 5 years or longer<br/>
2 = the patient died within 5 year

# References
1. Havlíček, Vojtěch, et al. "Supervised learning with quantum-enhanced feature spaces." Nature 567.7747 (2019): 209-212.<br/>
2. Schuld, Maria, and Francesco Petruccione. "Quantum ensembles of quantum classifiers." Scientific reports 8.1 (2018): 2772.<br/>
3. Pérez-Salinas, Adrián, et al. "Data re-uploading for a universal quantum classifier." Quantum 4 (2020): 226.<br/>
4. McKay, David C., et al. "Efficient Z gates for quantum computing." Physical Review A 96.2 (2017): 022330.<br/>
5. Dutta, Tarun, et al. "Single-qubit universal classifier implemented on an ion-trap quantum device." Physical Review A 106.1 (2022): 012411.<br/>
6. Fan, Liangliang, and Haozhen Situ. "Compact data encoding for data re-uploading quantum classifier." Quantum Information Processing 21.3 (2022): 87.<br/>
7. Qin, Ruiyang, et al. "Improving Quantum Classifier Performance in NISQ Computers by Voting Strategy from Ensemble Learning." arXiv preprint arXiv:2210.01656 (2022)<br/>
