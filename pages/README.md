**Note: These data are not yet available for general data requests.**

## About

The Tøien 2025 dataset is provided specifically to allow evaluation of a study where we tested two machine learning based sleep classifiers, proprietary Somnivore and open source Somnotate on polysomnographic data recorded from non-hibernating and undisturbed hibernating American black bears (*Ursus americanus*). The data set is provided to support the main findings of the study and is a small subset of a larger previously unpublished data set from the black bears. As automated scoring methods have not been applied to hibernating species before, a major concern is the potential effects of changing brain temperature on the EEG and the machine learning based detection. Therefore, we selected reference data from each of 6 bears, two one-day recordings at the highest and the lowest body temperatures during hibernation when body temperature (T<sub>b</sub>) was oscillating in multiday cycles, and a non-hibernating one-day recording in summer. We provide both the manual reference data scores, using consensus by 3 manual sleep scorers, and the resulting automated scores together with summaries of the scores. An early bioRxiv preprint of the accompanying study is available at  [doi: 10.1101/2025.03.31.646262](https://www.biorxiv.org/content/10.1101/2025.03.31.646262v1). The following details on the methods for data collection and scoring is a replicate of the method section in the accompanying study.

## Methods

### Data collection

The analyzed data were collected for monitoring purposes during a previous study, and the procedures for animal care and implantation of the telemetry transmitters are described by Tøien et al. (2015). These experiments were approved by the Institutional Animal Care and Use Committee at University of Alaska Fairbanks (IACUC nos. 05-56 and 08-64). Sleep related data from this data collection has not been published previously. Briefly, American black bears (*Ursus americanas*, 62-93 kg) were captured in Alaska by Alaska Department of Fish and Game (AD&G) during May–July, transferred to Fairbanks and held individually in an outdoor facility near the Institute of Arctic Biology in Fairbanks. The bears had been scheduled to be removed from the wild by ADF&G due to bear–human conflicts and would have been euthanized if not used by the project. In late August to late September in each year of the study, bears were immobilized with 8 mg/kg Telazol administered with a pole syringe and brought into surgery. Under isoflurane anesthesia and using aseptic protocol, the bears were implanted with telemetry devices (model T28F-14B, Konigsberg Instruments Inc., Pasadena, CA 91107) for measurement of T<sub>b</sub>, EKG, and deltoid muscle EMG. Using the same devices, global cortical EEG was recorded with a single differential pair of electrodes diagonally 1 cm from the skulls midline seam and 2 cm in front of and behind the bregma. The electrodes were stainless steel bone screws that penetrated into the extradural space and were insulated with acrylic cement. A single pair of EOG electrodes was implanted subcutaneously above the eyebrows. Some of the bears were also implanted with a blood pressure transducer in the caudal aorta. During recording, EEG, EOG and ECG channels were filtered with a 1-pole high pass (HP) filter at 0.1 Hz, and the EMG channel with 4-pole 20Hz HP filter. All of these channels were filtered with 3-pole low pass (LP) filters at 150Hz. Bears were also implanted with 2–3 intraperitoneal temperature data loggers for additional measurement of T<sub>b</sub> (TidbitT temp model UTBI-001, 0.06 °C resolution, Onset Computer Corporation Inc, Bourne, MA 02532). Both types of devices were calibrated against a mercury thermometer traceable to NIST standards in a water bath to an accuracy of 0.1 °C. During analysis additional digital filtering was applied as found appropriate by the manual sleep scorers, typically a 0.5 Hz 3rd order Butterworth HP filter for EEG and a 1 Hz first order Butterworth HP filter for EOG. 

Feeding was gradually removed over a two week period from mid October, and once showing signs of entering hibernation, the instrumented bears were transferred to undisturbed outdoor enclosures located in isolated forest lands near the Institute of Arctic Biology. The bears were maintained in artificial dens (91 × 97 × 98 cm inside dimensions, 865 L, constructed from welded 2.5 cm thick HD-polyethylene and insulated with 5cm Styrofoam) that functioned as respirometry chambers when the breakaway doors were kept closed. Breathing was recorded with total body plethysmography using custom designed differential pressure transducers based on Honeywell SDX05 pressure sensors with one side connected to the den interiors, and the reference side connected to spatial filters consisting of branched ca. 2 m long PP90 catheters ending about 1.5 m apart in the immediate vicinity of the dens. The pressure signals were LP filtered at 0.1Hz and also HP filtered with a 1000 s time constant that prevented long term drift off the baseline. Radio telemetry signals were received and decoded by a base station (Konigsberg TD14), and recorded at 500 Hz with a data acquisition system (CA recorder, DISS LLC). The originally recorded CArecorder files (now an obsolete file format) were translated to European Data Format (EDF) using custom code written in open source Lazarus Free Pascal by the first author, adapting the open source PUMA repository (Dr. Johannes W. Dietrich, Ruhr University of Bochum) to write large EDF files. Adhering to EDF/EDF+ standard, the data were split into animal specific 1 day long files and relevant metadata for the signals added.

### Manual scoring 

We selected from each of 6 bears three 24 h recordings: from mid-hibernation with a T<sub>b</sub> at the peak of a multiday body temperature cycle (Tøien at al. 2015)  from mid-hibernation near the trough of a T<sub>b</sub> cycle, and from a non-hibernating state either in early or late summer. These data were manually qualified by 3 different volunteer scorers. Scorers #1 and #3 had previous publication records in sleep research that included manual scoring of EEG data from mammals. Scorer #2 recorded all the data to be analyzed and had the longest experience with sleep data from hibernating bears, including the real-time observation of polysomnograms with video monitoring. None of these scorers were authors of the software that was used. As common in animal studies, we scored data into stages of NREM, REM, and Wake using 10 s epochs, and generally mapped what would be human stage N1, N2 and N3 to NREM, otherwise we used REM and Wake. We instructed scorers to not base scores on preconceptions about allowed transitions, i.e. not preventing Wake to REM transitions. In our preliminary analysis we also evaluated whether to also score a transition stage of Drowsiness with intermittent medium amplitude slow waves during inspirations occupying less than 50% of an epoch. However, we found difficulty in obtaining consistency among scorers, and it did not show consistent differences in and out of hibernation.

While we used the Polyman EDF reader as default viewer, we did not restrict use of other viewers or which additional channels that could be used for the manual scoring beyond EEG/EOG/EMG. Thus scorer #1 used Somnivore (with automatic scoring disabled) as viewer. Additional information from color spectral density arrays generated by the open source EDFbrowser (Teunis van Beelen, https://www.teuniz.net) was also used for assistance in the evaluation of the data. The scores were saved as separate EDF+ compliant files and were also exported in text format. From the qualifications of the 3 individual scorers we calculated consensus scores though a voting system using code written in Lazarus Free Pascal. The single set of consensus scores were used in the further software training and testing. Code used to generate the consensus scores from exported .csv files is available at https://github.com/otoien/ConsensusCode.

### Machine learning training

Due to the differences in design of the software, training differed between Somnivore and Somnotate. For training Somnivore we used 100 epochs of NREM, REM, and Wake randomly selected by the software from each file to be tested as per the design of the software. After an initial assessment we used only the EEG and EOG channels for training as the recorded EMG from the deltoid muscle showed very little activity in bears during hibernation, possibly due to the typical curled postures of the bears (Tøien et al. 2011) that causes stretching of the neck muscles. We applied a scoring rule of minimum consistency of 3 epochs for each of NREM, REM and Wake, which was necessary to approximate the sensitivity to changes in signal frequencies during transitions between states. Score Forcing that was an available option was not used to prevent Wake to REM transitions as it was found that spurious qualifications of short periods of Wake in the NREM to REM transition could affect what was correct detection of REM periods. 

Somnotate was trained on multiple complete one day recordings using the EEG and EOG channels. We used a time resolution of 10s (same as the epoch length), which was found to be a good compromise to prevent too high sensitivity to state changes during transition states. For initial assessment we used multiple training data sets. In non-holdout mode we used all the available data in a training data set, while in holdout mode we trained Somnotate with all the files in the training data set except the specific file to be tested. We created training models: a) based on a training data set with all the reference data, b) separate training data sets for hibernating and non-hibernating states, and c) separate training data sets for the files at high and low T<sub>b</sub> within the hibernating state. These were tested for overall accuracies in Somnotate. 

## Data overview

**Approved users can browse and [download the Tøien 2025 dataset here](:files_path:).**

**/Rawdata**

Main folder for polysomnographic recordings for each of 6 bears in EDF/EDF+ compliant format. Each bear is identified by subfolder names with a combination two-digit code for study year (start) and a single digit bear number of that study year. Example: "Bears08_Bear1". File names ending in .edf contain date of the recording in ISO format and bear number of the study year, and a –one to two letter code as follows: -HH hibernation at high T<sub>b</sub> (peak of a multiday body temperature cycle), -HL hibernation at low T<sub>b</sub> (trough of a T<sub>b</sub> cycle), -N non-hibernating. Example: Bear20120112a-Bear2-HH.edf. All other file names related to individual recordings follow a similar scheme. Channel information is contained in the metadata of each EDF file:

- ECG: Electrocardiogram to measure the electrical activity of the heart - lead 1 position.
- BP: Intra-aortic blood pressure (not present in Bears07 files).
- EEG: Electroencephalogram to measure the electrical activity of the brain.
- EOG: Electrooculography to measure eye movements by recording the electrical potential difference between the cornea and the retina.
- EMG: Electromyography to measure the electrical activity of muscles - recorded from neck/deltoid muscle.
- EMGamp: Derived rectified EMG with a low pass filtered time constant of 0.1 s.
- Resp: Qualitative breathing recorded with total body plethysmography.
- Tabd: Temperature of the telemetry transmitter. For Bears07 the implant site was intraperitoneal. The following seasons the implant site was subcutaneous on the lateral chest wall. 

**/Sleepscores**

Contains subfolders with sleep scores in EDF+ compliant format with file names using the .edf extension. Each subfolder contains a /CSV subfolder that contains the exported epochs in a single column text format. We use R&K scoring labels as supported for 10s epochs in the Polyman viewer as follows:

- Sleep stage 1: NREM (all sub stages)
- Sleep stage R: REM
- Sleep stage W: Wake
- Unscored: Score could not be determined (Somnivore standard label)

**/Sleepscores/AutoScores-Somnivore-EEGEOG**

Somnivore automated scores trained on 100 randomly chosen epochs of each kind from each file to be analyzed, using the EEG and EOG channels.

**/Sleepscores/AutoScores-Somnotate-EEGEOG**

Somnotate automated scores in non-holdout mode based on training separately on either all of the hibernation recordings or all summer recordings to be analyzed, using the EEG and EOG channels.

**/Sleepscores/ManualScores-Consensus**

Consensus of the individual manual scores using a voting system.

**/Sleepscores/ManualScores-EP**

Scores by manual scorer #1.

**/ManualScores-OT**

Scores by manual scorer #2.

**/ManualScores-YH**

Scores by manual scorer #3.

**/Summary**

- Bear-AutoScores-01.xlsx: Sleep stage occupancy of the data set.
- Bear-Auto-Scores-Accuracy-summary-01.xlsx: Overall scoring accuracies.
- Bear-Consensus-summary-States-01.xlsx: Summary of individual scorer's agreement with the consensus scores. 
- Bear-Somnivore-Somnotate-comp-vs-Consensus-F-measure-01.xlsx: F-measures of Somnivore and Somnotate automated scores vs. Consensus scores.

## Access and usage restrictions

The Toien 2025 dataset is only available for non-commercial use to evaluate the accompanying study.

## Citation and acknowledgement

When using this dataset, users must cite the following:

> [Zhang GQ, Cui L, Mueller R, Tao S, Kim M, Rueschman M, Mariani S, Mobley D, Redline S. The National Sleep Research Resource: towards a sleep data commons. J Am Med Inform Assoc. 2018 Oct 1;25(10):1351-1358. doi: 10.1093/jamia/ocy064. PMID: 29860441; PMCID: PMC6188513.](https://pubmed.ncbi.nlm.nih.gov/29860441/)

Users must include the following text in any Acknowledgements:

> The data set being analyzed was supported by U.S. Army Medical Research and Materiel command awards W81XWH-06-1-0121 and W81XWH-09-2-0134 and NSF award number: IOS1147232. The analysis was supported by an Institutional Development Award (IDeA) from the National Institute of General Medical Sciences of the National Institutes of Health under Awards Number P20GM103395 (INBRE) and P20GM130443 (COBRE). The content is solely the responsibility of the authors and does not necessarily represent the official views of the National Institutes of Health. The National Sleep Research Resource was supported by the U.S. National Institutes of Health, National Heart Lung and Blood Institute (R24 HL114473, 75N92019R002).

## Changelog

*September 2025*

- Make Toien 2025 dataset available for data requests

## References

- [Tøien Ø, Blake J, Edgar DM, Grahn DA, Heller HC, Barnes BM. Hibernation in black bears: independence of metabolic suppression from body temperature. Science 2011;331: 906-9.](https://pubmed.ncbi.nlm.nih.gov/21330544/)
- [Tøien Ø, Blake J, Barnes BM. Thermoregulation and energetics in hibernating black bears: metabolic rate and the mystery of multi-day body temperature cycles. J Comp Physiol. B 2015;185: 447-61.](https://pubmed.ncbi.nlm.nih.gov/25648622/)
- Toien 2025 GitHub Documentation: https://github.com/nsrr/toien-2025-documentation

## Questions?

Please reach out to us at support@sleepdata.org or in the [Forum](https://sleepdata.org/forum) if you have questions.
