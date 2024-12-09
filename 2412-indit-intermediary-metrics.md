# Indit Intermediary Metrics

**links**
* task https://neconcoimmunity.atlassian.net/browse/ID-294?searchObjectId=23410&searchContainerId=10025&searchContentType=issue&searchSessionId=60960069-9596-4f46-8bd2-a6c67b508d70
* v2 model feature importance https://neconcoimmunity.atlassian.net/wiki/spaces/RD/pages/1249968165/Final+model+v2.0+-+Expressionless#Training-feature-importance
* process model documentation https://neconcoimmunity.atlassian.net/wiki/spaces/RD/pages/1460371500/Processing+Models+Patent

**task**
- [ ] Explore and familiarize yourself with output files on cepi9 for influenza protein in cursor file explorer

**maybe later**
- [ ] Set up a meeting with Peyman for the metrics
    - [ ] Come up with a draft list of metrics to include
    - [ ] Define a goal for the meeting with Peyman

## Meeting with Ghazal

## v2 AP models (paused ❌)
Is it time to upgrade to V2 models? 
Ghazal's recommended I read this to gauge the feature importance
for my metrics https://neconcoimmunity.atlassian.net/wiki/spaces/RD/pages/1249968165/Final+model+v2.0+-+Expressionless#Training-feature-importance.
It is for v2 models.

Should we discuss this in the meeting on Tuesday?
How do I go aboud validating that upgrade?
If so I think the upgrade to V2 models task should come before this as a separate task because
it feels independent.
All analyzis work from Peyman will have been done on v2 models.

int-int change log has 1.6-v.2.0 on a high level, what models and stuff changed 
https://neconcoimmunity.atlassian.net/wiki/spaces/RD/pages/1195376663/Int-int+change-log
Seems they haven't changed the output to be a probability yet?

I think my job should be to upgrade the model. Do some sanity testing. And then someone
more familiar with the output should run validation.
I want to just try bumping the image we use in the antigen predictor to see if it
still runs?
And you can diff the output if you run it for your one simple protein?

### Aga: Scope and impact of bumping AMB models to 2.4

**Conclusion**: 
Focus on the intermediary metrics pruning and getting a good set of output names
for all_scores first.

Bumping AP models is a larger project. And we need to sync with DS first. The meeting
with DS should be something like:
Hey we use these exact models. (with some work from you to figure out exactly what we're using)
What should we be using instead?

And the brunt of the work with upgrading models is to come up with a **validation strategy** of our own.
We need to know what our processing on top of the AP scores behaver well.
And that our workflow tests make sense.
Snapshot tests feel like they could be nice for this.

Simen is back in January. Maybe it would be good to wait and ask him?
Marius is leaving end of next week. Might be good to get some input from him on what approach he would do
for validating indit output with AP scores from the new models.


**notes**
indit is based on covid_mutant. It still does a bit of processing stuff, but likely not the main
AP prediction. (you could update the docs here to explain this better)
Runar optimized indit to run some of the model AMB and neunethlabind outside of covid_mutant https://github.com/OncoImmunity/indit/pull/10

Simen was telling them to wait with upgrading back in 2023, but then he dropped the ID mettings and it was left
in an unclear state.
We found this issue for a thing that blocked us from upgrading AMB models. The issue is still open, we don't know
if it is still relevant. It seems related to our direct use of neunethlabind image(RNN_IMAGE)
Add support for using resert binding predictions: https://neconcoimmunity.atlassian.net/browse/ID-42

The repo called prediction-runner is what used to run AMB for PCV. We're
not sure where/how AMB is run for PCV now.

In theory you can merge larger changes to indit without validating manually, since
new project shoudl use the tagged version of indit.
But Aga fears that people will normally just use the latest and then be burnt.

We have lab validation data for 1.6. If the prediction have changed with 2.4 it is not clear
how we can then validate the new predictions.

We looked at the feature contribution change between 1.6 and 2.0.
The feature set looks very similar with some shifting up and down. 
https://neconcoimmunity.atlassian.net/wiki/spaces/RD/pages/1249968165/Final+model+v2.0+-+Expressionless#Trained-models
Probably the model bump does not change what we would want to store as our final predictions
that much at all.

The goal for the intermediary metrics task is a short term goal of not storing so much junk for all our projects.
We decide what we write to disk in intermediary results. We don't think these files and which we store will
be much affected, if there are changes it will likely just be column names.

Aga would approach the task this way:
What are the intermediate predictions we output now?
Make a map/list we want to store that could be important to keep for later refefence.
Then ask DS people for input on this. What is actually important?

So this task is mainly about pruning intermediary scores.
Aga's intuition: keep binding, processing, all predictions.

To run indit with an updated package version for fex covid_mutant.
Build and tag a local image, updated constants.py in indit to use the local
image. Then run indit.

## AP feature explanations from Peyman
https://app.slack.com/client/T0L3DL1DL/D0830H5BF0W
> Here is the link to AP explanations. In the report pdfs, please rely on explanations of the second column (i.e., Approach 2) 
https://neconcoimmunity.atlassian.net/wiki/spaces/RD/pages/1739882509/Antigen+Presentation+XAI+Report
There is a notebook for producing the report https://github.com/OncoImmunity/explanation-notebooks/blob/main/ap_xai_report.ipynb

![](2024-12-02-10-27-07.png)
So our goal is to see what features contribute to the high AP score predictions we make?

nr_positivies 200-600k?
nr_negatives = nr_positives * 1000?
I vaguely remember Ghazal saying 1k. Looking in int-data-preparation I see training_ration of 1000
https://github.com/OncoImmunity/int-data-preparation/blob/master/config/nec.yaml but I don't know if this is
the neg:post ration number.

xgbfp_chrrep13
![](2024-12-02-15-09-34.png)
ic50_resert, proc12, ic50_rnn

## Mapping the intermediary output from my indit run

