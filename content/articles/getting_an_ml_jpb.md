---
title: 'Notes on: Getting an ML job'
date: 2024-05-23T13:07:04+01:00
date: "2024-05-23"
draft: false
readTime: true
toc: true
---

[Summary of this article / video](https://www.mrdbourke.com/get-a-machine-learning-job/)

### Intro
- can split getting an ML job into 2 steps:
	1. Getting ML skills
		- building projects
		- contributing to OS
		- reading technical info
	1. Marketing ML skills
		- communication
		- [interviewing](https://huyenchip.com/ml-interviews-book/)
		- portal creation
		- passing application screening

### Strategies:
**Make ML jobs come to you by [Learning in Public](https://www.swyx.io/learn-in-public)** (great article!)
Summary:
- write blogs / tutorials / cheatsheets
- answer things on stackoverflow / reddit
- make videos
- draw [cartoons](https://code-cartoons.com/)
- Pull Request libraries you use
- OS: github repo -> issues -> 'good first issue' (easy ones to solve)
- make your own libraries intended only for you
- goto conferences
==> **make the thing you wish you had found**

{{< notice info >}}
Becoming an Expert:
Take on concrete projects and accomplish **depth-wise**
Teach/Summarise what you learn
{{< /notice >}}


ALSO.. [Learning in Private (Great Article)](https://www.swyx.io/learn-in-private) when its applicable
- fork repos just to look at the code
- follow *people* not algorithms (RSS feeds)
- Personal Knowledge Management
- Spaced Repetition (Anki)
- Active, not Reactive Learning

{{< notice tip >}}
"*80% of developers are “dark”, they don't write or speak or participate in public tech discourse. But you do. You must be an expert, right? Don’t tell them you aren’t. Answer best as you can, and when you’re stuck or wrong pass it up to your mentors.*"
{{< /notice >}}


{{< notice tip >}}
#### [Publishing your work increases your luck](https://github.com/readme/guides/publishing-your-work)
{{< /notice >}}

### [Doing the job before you have it](https://www.mrdbourke.com/how-can-a-beginner-data-scientist-like-me-gain-experience/)
example:
- job where a project involved identifying if a surgeon's tool was on the operating table
- BUT, job required 3+ years experience
- guy decided to create his own training set, and make the model himself
- best case: company loves it, worst case: another project to show off
- Deploy Proof of Concept on Streamlit, Gradio, HF Spaces (so it has a nice front end)


### Be [So Good They Can't Ignore You](https://whatyouwilllearn.com/wp-content/uploads/2018/02/Summary-of-SGTCIY-pdf.pdf)
linked is a summary
- be a craftsman, create meaningful things, and *luck* will come
- don't follow the ambiguous "*Passion*", just focus on what interests you right now
- strain: stretch your abilities
#### 5 Habits of a Craftsman
1. Decide what type of capital market you are in
	- Winner take all = only the best in the field will reap the rewards. There is only one type of skill and only the best will be compensated.
	- Auction = there are multiple different types of skills, and you can bid with the skills that form your own personal strengths
2. Identify your capital type
	- Seek ‘open gates’ - these are opportunities already open to you that will allow you to build career capital. These may be specific project you could w
	- ork on, specific individuals to collaborate with, or specific opportunities that will allow you to develop valuable skills
	- Skill acquisition is like the momentum of a freight train: “Getting starting requires a huge application of effort, but changing track once it’s moving it easy”
3. Define ‘Good’
	- Now that you’ve identified the skill you need to build, you need to know what ‘good’ is (as in ‘so good they can’t ignore you) and set goals along the way that will take you from your current ability to ‘good’
4. Stretch and Destroy
	- “Deliberate practice is above all an effort of focus and concentration”
	- “Deliberate practice is often the opposite of enjoyable”
	- You need to strain and stretch your abilities in order to grow, and in the process, you destroy your previous idea of what ‘good’ was and form a new, higher level of what you need to achieve
5. Be Patient
	- Developing ‘good’ skills is hard. Because of this, we need to look into the future for the payoff, not expect it to happen quickly.

### Having a good resume
[What we look for in a resume](https://huyenchip.com/2023/01/24/what-we-look-for-in-a-candidate.html)
**Every company hires differently**
-> especially Big vs Little companies
	-> Startups more likely to read manually, huge companies will certainly use AI
- long lists of skills might hurt your resume- its unlikely someone is expert, or even profficient, at 20+ things
- although this might help pass automated screening, a human will eventually need to review the resume, make sure it passes them too
- This HM (hiring manager) looks for **Demonstrated Knowledge**
- if you list common skills like git / jupyter notebook as your skill, the HM will assume you have weak skills

{{< notice info >}}
###### The Advantage of demonstrated expertise
*"Consider these two candidates who both mention Flink on their resumes. Which one would you want to talk to?*

- *Candidate A has Flink as one of the 30 items on their Technical skills box.*
- *Candidate B explained how they used Flink in their last job: “worked on a feature computation platform built on top of Apache Flink which processes 100,000 events per second and serves 10 different ML models.”*

*If during our interview, candidate B can tell me why they chose Flink over other stream processing engines, what issues they’ve encountered, and what changes they wish to see in Flink, I’d be sold!"*
{{< /notice >}}

- traits HM looks for in candidates:
	- Initiative
	- Persistance
- if you can demonstrate this, include it in your resume

- Don't waste resume space listing cookie-cutter projects:
	- titanic, sentiment analysis of tweets, stock trading, chatbots
- these are good to practice on, but wont help you stand out
- Quantifying isnt always good, **it needs context**
	- if you cant easily quantify something, forcing it wont be useful
	- instead, talk about how it made you a better engineer (for example)
- if talking about metrics, talk about both:
	- how they can be tied to buisness objectives
	- your contribution to acheiving that metric

{{< notice info >}}
###### Good Example Metrics
Here are some of the metrics that we’ve found convincing:

- Part of a 2-data-scientist team that owns feature engineering for a fraud detection system. Added 200 new features, resulting in a reducing the false positive rate from 20% to 15%, while keeping the false negative the same.
- Built caching strategy using application-level caching & Redis for 2000 QPS, leading to a decrease in response time by 50%.
{{< /notice >}}

{{< notice tip >}}
The one-page limit suggestion is to help you be concise. Like the French mathematician Blaise Pascal once said: “_I have only made this letter longer because I have not had the time to make it shorter_.” **The longer your resume goes on, the more chance that your biggest strengths will be buried among less important details.**

"The goal of a resume is not to show _everything_ about you. The goal is to put your best foot forward to show a company why you’d be an excellent addition to their team. **Rarely do I see a candidate whose best foot forward can’t be contained within one page**."
{{< /notice >}}
## Interviews
Highly Recommended (free) [Introduction to Machine Learning Interviews Book](https://huyenchip.com/ml-interviews-book/)

## Misc
### Do I need a cover letter?
(excerpt)
"*The order in which I read an application: resume -> cover letter. If you have stellar experience and skills, we’d want to talk to you even if you don’t have a cover letter. Some hiring managers told me that they don’t read cover letters at all.*

*I, however, do appreciate it when a candidate writes a cover letter that explains why they want to join us and why they think they’re a good fit for the role. For candidates with unusual transitions (e.g. switching from another career into machine learning), a cover letter could also be a great place to explain their transition.*

*If you write a cover letter, keep it concise. A cover letter doesn’t have to be a PDF. It can just be an email.*

*If an information is important, include it in your resume instead of a cover letter. Sometimes, candidates put the important info in the email they sent to our team’s email address, which might not be entered correctly into our application tracking system.*"

### Misc Tips

##### General

1. If you’re applying to a small startup, say, of less than 20 people, spend some time researching who works at that startup and email them directly.
2. Send your resume as a PDF instead of an editable format like Microsoft Word or Google Docs. The editable format might not render correctly on other people’s computers.
3. If you can get someone who used to supervise you to talk about how great you are, include their quote in your resume. Quotes from friends/family don’t count.
4. Don’t use abbreviations unless you know for sure your audience knows what you’re talking about.
##### Public links

1. If you’ve contributed to open source projects, include links to the PRs or a public architectural design you’re the most proud of.
2. If your GitHub has a lot of repos, pin the important ones on your homepage (you can pin up to 6). You can also write a README to guide your visitors on what repos they would look at.
3. Don’t include a link to your GitHub link if it’s empty.
4. If you have publications, link to your Google Scholar profile.
5. If you’re a co-author of a paper with multiple authors, bold your name in the author list.
6. If you have more to show than your resume allows, create a personal website. Assuming that you have basic coding skills, it’s fairly easy to create a free personal website using GitHub Pages.
##### Education

1. If you’re still in school, put education earlier in your resume, as it helps the person screening your resume knows where you are and what you’re looking for. If you’ve been working, put your work experience first.
2. If you’re still in school, list your expected graduation date so companies know when you can start working full-time.
3. If you’ve been working for 2+ years, remove your GPA and coursework. I care more about your work experience.
4. Similarly, course projects should only be listed if you think they’re better than the average course project.

