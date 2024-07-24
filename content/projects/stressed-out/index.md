+++
title = "Stressed out"
template = "project.html"

[extra]
subtitle = "computational linguistics research"
role = "Primary author/researcher"

tags = ["NLP", "Machine Learning", "Speech Processing"]
tech = ["Python", "Praat", "SciKit"]

links = [
    { title = "Interspeech paper", href = "https://www.isca-archive.org/interspeech_2015/paul15_interspeech.pdf" },
    { title = "AVSP paper", href = "https://www.isca-archive.org/avsp_2015/bethamcherla15_avsp.pdf" }
]

team_name = "Co-authors"
team = [
    { name = "Cecilia Ovesdotter Alm", link = "http://tinyurl.com/ceciliaoalm/" },
    { name = "Joe Geigel", link = 'https://www.cs.rit.edu/~jmg/' },
    { name = "Reynold Bailey", link = "https://www.cs.rit.edu/~rjb/" },
    { name = "Linwei Wang", link = "http://people.rit.edu/lxwast/Linwei_Wangs_HomePage/Home.html" },
    { name = "Vasudev Bethamcherla" }
]
+++

Stress can have a negative and costly impact on people’s lives. Mitigating stress before it becomes a problem requires early, noninvasive identification and a deeper understanding of the signals of stress. To test automatic stress detection we created a new dataset with subjects completing the Stroop task under unstressed and stressed conditions. We then used supervised classification algorithms to try to discriminate between the stressed and unstressed condition.

Features were extracted from recorded speech data and trained with several classification algorithms. We explored binary classification of stressed vs. unstressed across gender and per gender, with the best results on a held-out test set improving over the majority class baseline (MCB) by 16% across genders and with 20% and 21% for the female and male subsets respectively. Overall maximum intensity emerged as the most informative feature when comparing across classification conditions. In addition, we explored leave-one subject out classification, resulting in a 15% improvement on average considering both genders when using random forests.

I was a primary author on two papers that came out of this project and presented them at Interspeech 2015 in Dresden and FAAVSP 2015 in Vienna.

