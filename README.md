# jAlergia - Alergia passive automaton learning
<hr>
**jAlergia** is minimal and efficient implementation of ALERGIA automaton learning algorithm in Java. 
It is developed without any dependencies and can be used either in code or from command line. 

Learned models are saved in the .dot format and can be visualized with [graphviz](https://graphviz.org/) and used with [AALpy](https://github.com/DES-Lab/AALpy).
AALpy also includes python bindings to jAlergia .jar file.

jAlergia supports passive learning of
- [Markov Decision Processes](https://en.wikipedia.org/wiki/Markov_decision_process)
- [Stochastic Mealy Machines](https://link.springer.com/chapter/10.1007/978-3-030-92124-8_27)
- [Markov Chains](https://en.wikipedia.org/wiki/Markov_chain)

# Usage

### Command line
```
git clone https://github.com/emuskardin/jAlergia
gradlew jar
# gradlew.bat on Windows
java -jar alergia.jar -path sampleFiles/mdpData1.txt -type mdp
or
java -jar alergia.jar -help // for more details
# in case you run out of memory during FPTA construction, extend it with -Xmx12g
```

### In code
```java
class AlergiaExample {
    public static void main() {
        String path = "sampleFiles/mdpData2.txt"; // path to input file
        double eps = 0.005; // epsilon used in Hoeffding compatibility check
        ModelType type = ModelType.MDP;
        String saveLocation = "jAlergiaModel";
        OptimizeFor optimizeFor = OptimizeFor.ACCURACY; // learn as precise as possible

        Alergia a = new Alergia(path, eps, type, saveLocation, optimizeFor);
        a.runAlergia();
    }
}
```

### Integration with AALpy

Model learned by jAlergia can be loaded and visualized by AALpy, 
an open source active automata learning library written in Python.

```python
from aalpy.learning_algs import run_JAlergia
from aalpy.utils import visualize_automaton

# if you need more heapreplace check
model = run_JAlergia(path_to_data_file='jAlergia/exampleMdpData.txt', automaton_type='mdp', eps=0.005,
                     path_to_jAlergia_jar='jAlergia/alergia.jar')

visualize_automaton(model)
```

## Cite AALpy and Research Contact

jAlergia is a twin implementation of [AALpy's Alergia implementation](https://github.com/DES-Lab/AALpy/blob/master/aalpy/learning_algs/stochastic_passive/Alergia.py),
and it is maintained as a part of the please cite:
AALpy library. If you use jAlergia in the research context, please cite:
```
@inproceedings{aalpy,
	title = {{AALpy}: An Active Automata Learning Library},
	author = {Edi Mu\v{s}kardin and Bernhard K. Aichernig and Ingo Pill and Andrea Pferscher and Martin Tappler},
	booktitle = {Automated Technology for Verification and Analysis - 19th International
	Symposium, {ATVA} 2021, Gold Coast, Australia, October 18-22, 2021, Proceedings},
	series    = {Lecture Notes in Computer Science},  
	publisher = {Springer},
	year      = {2021},
}
```
If you have research suggestions, or you need specific help concerning your research, feel free to start a [discussion](https://github.com/DES-Lab/AALpy/discussions) or contact [edi.muskardin@silicon-austria.com](mailto:edi.muskardin@silicon-austria.com).
We are happy to help you and consult you in applying automata learning in various domains.
se open issues.