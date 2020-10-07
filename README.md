<p align="center">
<img alt="Dioscuri logo" title="Dioscuri" src="https://raw.githubusercontent.com/Edinburgh-Genome-Foundry/Dioscuri/master/images/Dioscuri.png" width="140">
</p>


# Dioscuri

Dioscuri is a Python package for working with **Gemini WorkList** (gwl) files and objects.

A Gemini worklist file is a text file that contains pipetting instructions for the Tecan Freedom EVO robots. Dioscuri uses the Freedom EVOware (v2.7) software's specification of the gwl format.


*Dioscuri* is a name for Castor and Pollux, the twins who were transformed into the Gemini constellation in Greek mythology.


## Install

```bash
pip install dioscuri
```


## Usage
```python
import dioscuri

aspirate = dioscuri.Pipette(operation="Aspirate",
                            rack_label="Source1",
                            rack_type="4ti-0960/B on raised carrier",
                            position="3",
                            volume="50")
aspirate.to_string()

dispense = dioscuri.Pipette(operation="D",
                            rack_label="Destination",
                            rack_type="4ti-0960/B on CPAC",
                            position="1", 
                            volume="50")

wash = dioscuri.WashTipOrReplaceDITI()

worklist = dioscuri.GeminiWorkList(name="my_worklist",
                                   records=[aspirate, dispense, wash])
worklist.records_to_string()

print(worklist.records_to_string())
# A;Source1;;4ti-0960/B on raised carrier;3;;50;;;;
# D;Destination;;4ti-0960/B on CPAC;1;;50;;;;
# W;
```

The generated string can be saved in a text file:

```python
with open("picklist.gwl", "w", encoding='utf8') as f:
    f.write(worklist.records_to_string())
```


## Versioning

Dioscuri uses the [semantic versioning](https://semver.org) scheme.


## License = MIT

Dioscuri is [free software](https://www.gnu.org/philosophy/free-sw.en.html), which means the users have the freedom to run, copy, distribute, study, change and improve the software.

Dioscuri was written at the [Edinburgh Genome Foundry](https://edinburgh-genome-foundry.github.io/) by [Peter Vegh](https://github.com/veghp) and is released under the MIT license.
