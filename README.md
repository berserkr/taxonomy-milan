# InstructLab 🥼 Taxonomy

## Contents 📖 

- [Welcome to the InstructLab Taxonomy](#welcome-to-the-instructlab-taxonomy)
- [Learning](#learning)
- [Getting Started with Skill Contributions](#getting-started-with-skill-contributions)
  - [Skills: YAML examples](#skills-yaml-examples)
- [Getting Started with Knowledge Contributions](#getting-started-with-knowledge-contributions)
  - [Knowledge: YAML examples](#knowledge-yaml-examples)
- [Taxonomy tree layout](#taxonomy-tree-layout)
- [Contribute knowledge and skills to the taxonomy!](#contribute-knowledge-and-skills-to-the-taxonomy)
  - [Ways to contribute](#ways-to-contribute)
  - [Detailed Contribution Instructions](#detailed-contribution-instructions)
## Welcome to the InstructLab Taxonomy

InstructLab 🥼 uses a novel synthetic data-based alignment tuning method for
Large Language Models (LLMs.) The "**lab**" in Instruct**Lab** 🥼 stands for
**L**arge-scale **A**lignment for Chat **B**ots.

The LAB method is driven by taxonomies, which are largely created manually and
with care.

This repository contains a taxonomy tree that allows you to create models
tuned with your data (enhanced via synthetic data generation) using LAB 🐶
method.

## Learning

Learn about the concepts of "skills" and "knowledge" in our [InstructLab Community Learning Guide](https://github.com/instruct-lab/community/blob/main/docs/README.md).

## Getting Started with Skill Contributions

Skills require a much smaller volume of content than knowledge contributions. An entire skill contribution to the taxonomy tree can be just a few lines of YAML in the `qna.yaml` file ("qna" is short for "questions and answers") and an `attribution.txt` file for citing sources. 

Your skills contribution pull requests must include the following:
- A `qna.yaml` that contains a set of key/value entries with the following keys
  - Each `qna.yaml` file requires a minimum of five question and answer pairs.
- A `attribution.txt` that includes the sources for the information used in the `qna.yaml`

> [!TIP]
> The skill taxonomy structure is used in several ways:
>    1. To select the right subset of the taxonomy to use for data generation.
>    2. To determine the interpretability by human contributors and maintainers.
>    3. As part of the prompt to the GPT model used to generate synthetic samples.

> [!NOTE]
> To get the best use of this structure, make sure the names of directories match the intent of the
> taxonomy files. You can also verify that a person's contribution is in the most logical location in the
> taxonomy structure before signing off.

Taxonomy skill files must be a valid [YAML](https://yaml.org/) file named `qna.yaml`. Each `qna.yaml` files contains a set of key/value entries with the following keys:

- `task_description`: A description of the skill. This key is required.
- `created_by`: The GitHub username of the contributor. This key is required.
- `seed_examples`: A collection of key/value entries. New
  submissions should have at least five entries, although
  older files may have fewer. This key is required.
  - `context`: Grounded skills require the user to provide context containing information that the model is expected to take into account during processing. This is different from knowledge, where the model is expected to gain facts and background knowledge from the tuning process. The context key is optional for freeform skills.
  - `question`: A question for the model. This key is required.
  - `answer`: The desired response from the model. This key is required.

Other keys at any level are currently ignored.

### Skills: YAML examples

To make the `qna.yaml` files easier and faster for humans to read, it is recommended to specify `task_description` first, followed by `created_by`, and finally `seed_examples`.
In `seed_examples`, it is recommended to specify `context` first (if applicable), followed by `question` and `answer`.

*Example `qna.yaml`*
```yaml
task_description: <string>
created_by: <string>
seed_examples:
  - question: <string>
    answer: |
      <multi-line string>
  - context: |
      <multi-line string>
    question: <string>
    answer: |
      <multi-line string>
  ...  
```

Then, you create an `attribution.txt` file that includes the sources of your information.

*Example `attribution.txt`*
```
1. [Link to source]
2. [Link to source 1], [Link to source 2] 
3. Self-authored
```

If you have not written YAML before, don't be intimidated - it's just text.

> [!TIP]
> - Spaces and indentation matter in YAML. Two spaces to indent.
> - Don't use tabs!
> - Be careful to not have trailing spaces at the end of a line.
> - Each example in `seed_examples` begins with a "-". Place this "-" in
  front of the first field (`question` or `context`). The remaining keys in the
  example should not have this "-".
> - Some special characters such as " and ' need to be "escaped." This is why some
  of the lines for keys in the example YAML we provided have the '|' character.
  This character escapes all of the special characters in the value for the key.
  You might also want to use the '|' character for multi-line strings.

It is recommended that you **lint**, or verify your YAML using a tool. One linter option is [yamllint.com](https://yamllint.com). You can copy/paste your YAML into the box and click **Go** to have it analyze your YAML and make recommendations. Online tools like [prettified](https://onlineyamltools.com/prettify-yaml) and [yaml-validator](https://jsonformatter.org/yaml-validator) can automatically reformat your YAML to adhere to our `yamllint` PR checks, such as breaking lines longer than 120 characters.

#### Freeform compositional skill: YAML example

```yaml
task_description: 'Write Haikus.'
created_by: juliadenham
seed_examples:
 -  question: Write me a 5-7-5 Haiku.
    answer: |
     The wind of Fuji
     I've brought on my fan
     a gift from Edo.
 - question: Write me a 5-7-5 Haiku.
   answer: |
     A blanket of fog
     Engulfs the world around me
     A dreary springtime.
 - question: Write me a 5-7-5 Haiku.
   answer: |
     Bright, the near-full Moon
     Craters look like gray flowers
     Listen, Crickets call.
 - question: Write me a 5-7-5 Haiku.
   answer: |
     The west wind whispered,
     And touched the eyelids of spring,
     Her eyes, Primroses.
 - question: Write me a 5-7-5 Haiku.
   answer: |
     Introverts at home
     Are plagued by hyper children
     When will school start next?
```

Seriously, that's it.

Here is the location of this YAML in the taxonomy tree. Note that the YAML file
itself, plus any added directories that contain the file, is the entirety of the skill
in terms of a taxonomy contribution:

#### Freeform compositional skill: Directory tree example

```ascii
[...]

└── writing
    └── freeform
    |   └── haikus <=== here it is :)
    |   |   └── qna.yaml
    |   |       attribution.txt 
    │   ├── debate
    │   │   └── qna.yaml
    |   |       attribution.txt   
    │   ├── legal
    │   │   ├── agreement
    │   │   |    └── qna.yaml
    |   |   |        attribution.txt
[...]
```

#### Grounded compositional skill: YAML example

Remember that [grounded compositional skills](https://github.com/instruct-lab/community/blob/main/docs/SKILLS_GUIDE.md) require additional context and include a `context` field. 

This example snippet assumes the GitHub username `mairin` and shows some of the question/answer pairs present in the actual file:

```yaml
task_description: | 
    This skill provides the ability to read a markdown-formatted table.
created_by: mairin # Use your GitHub username; only one creator supported
seed_examples:
  - context: |
      | **Breed**      | **Size**     | **Barking** | **Energy** |
      |----------------|--------------|-------------|------------|
      | Afghan Hound   | 25-27 in     | 3/5         | 4/5        |
      | Labrador       | 22.5-24.5 in | 3/5         | 5/5        |
      | Cocker Spaniel | 14.5-15.5 in | 3/5         | 4/5        |
      | Poodle (Toy)   | <= 10 in     | 4/5         | 4/5        |
    question: |
      Which breed has the most energy?
    answer: |
      The breed with the most energy is the Labrador.
  - context: |
      | **Name** | **Date** | **Color** | **Letter** | **Number** |
      |----------|----------|-----------|------------|------------|
      | George   | Mar 5    | Green     | A          | 1          |
      | Gráinne  | Dec 31   | Red       | B          | 2          |
      | Abigail  | Jan 17   | Yellow    | C          | 3          |
      | Bhavna   | Apr 29   | Purple    | D          | 4          |
      | Rémy     | Sep 9    | Blue      | E          | 5          |
    question: |
      What is Gráinne's letter and what is her color?
    answer: |
      Gráinne's letter is B and her color is red.
  - context: |
      | Banana | Apple      | Blueberry | Strawberry |
      |--------|------------|-----------|------------|
      | Yellow | Red, Green | Blue      | Red        |
      | Large  | Medium     | Small     | Small      |
      | Peel   | Peel       | No peel   | No peel    |
    question: |
      Which fruit is blue, small, and has no peel?
    answer: |
      The blueberry is blue, small, and has no peel.
```

#### Grounded compositional skill: Directory tree example

```ascii
[...]

└── extraction
    └── inference
    |   └── qualitative
    |   |    ├── sentiment
    |   |    |    └── qna.yaml
    |   |    |        attribution.txt 
    |   |    └── tone_and_style
    |   |         └── qna.yaml
    |   |             attribution.txt
    │   ├── quantitative
    │   │   ├── table_analysis <=== here it is :)
    │   |   |    └── qna.yaml
    │   │   │        attribution.txt
    │   │   ├── word_frequency
    │   │   │   └── qna.yaml
    │   │   │        attribution.txt
[...]
```
## Getting Started with Knowledge Contributions

While skills are foundational or performative, knowledge is based more on answering questions that involve facts,
data, or references.

Knowledge in the taxonomy tree consists of a few more elements than skills:

- Each knowledge node in the tree has a `qna.yaml`, similar to the format of the `qna.yaml` for skills. 
- ⭐ Knowledge submissions require you to create a repository, can be with GitHub, that contains the markdown files of your knowledge contributions. These contributions in your repository must use the markdown (.md) format.
- The `qna.yaml` includes parameters that contain information from your repository. 

> [!TIP] 
> Guidelines for Knowledge contributions
> - Submit the most up-to-date version of the document
> - All submissions must be text, images will be ignored
> - Tables can be added 

Each `qna.yaml` file requires a minimum of five question-answer pairs. The `qna.yaml` format must include the following fields:
ˇ
- `task_description`: An optional description of the knowledge.
- `created_by`: Your GitHub username.
- `domain`: Category of the knowledge. 
- `seed_examples`: Five or more examples sourced from the provided knowledge documents.
  - `question`: A question for the model. This key is required.
  - `answer`: The desired response from the model. This key is required.
- `document`: The source of your knowledge contribution.
  - `repo`: The URL to your repository that holds your knowledge markdown files.
  - `commit`: The SHA of the commit in your repository with your knowledge markdown files.
  - `patterns`: A list of glob patterns specifying the markdown files in your repository. Any glob pattern that starts with `*`, such as `*.md`, must be quoted due to YAML rules. For example, `"*.md"`.

### Knowledge: YAML examples
```yaml
task_description: 'Teach the model the results of the 2024 oscars'
created_by: juliadenham
domain: pop_culture
seed_examples:
 - question: When did the 2024 oscars happen?
   answer: |
     The 2024 oscars were held on March 10, 2024.
 - question: What film had the most oscar nominations in 2024?
   answer: |
     Oppenheimer had 13 oscar nominations.
 - question: Who presented the awards for Best Original Screenplay and Best Adapted Screenplay?
   answer: |
     Octavia Spencer.
 - question: Who hosted the 2024 oscars?
   answer: |
     Jimmy Kimmel hosted the 96th Academy Awards ceremony.
 - question: At the 2024 Oscars, who were the nominees for best director and who won?
   answer: |
     The nominees for director at the 2024 oscars was Christopher Nolan for Oppenheimer,
     Justine Triet for Anatomy of a Fall, Martin Scorsese for Killers of the Flower Moon,
     Yorgos Lanthimos for Poor Things, and Jonathan Glazer for The Zone of Interest.
     Christopher Nolan won best director for Oppenheimer.
 - question: Did Billie Eilish perform at the 2024 oscars?
   answer: |
     Yes Billie Eilish performed "What Was I Made For?" from Barbie.
document:
 repo: https://github.com/juliadenham/oscars2024_knowledge.git
 commit: a22148c
 patterns:
   - oscars2024_results.md
```
This knowledge example references one markdown file: `oscars2024_results.md`. You can also add multiple files for knowledge contributions. 

> [!NOTE]
> Due to the higher volume, **it will naturally take longer to receive acceptance for
> a knowledge contribution pull request than for a skill pull request**. Smaller
> pull requests are simpler and require less time and effort to review.

What might these markdown files look like? They can be freeform. Here's what a
snippet of `oscars2024_results.md` might look like in your git repository.

#### Knowledge: Freeform example

```markdown
# 96th Academy awards

The **96th Academy Awards** ceremony, which was presented by the
[Academy of Motion Picture Arts and
Sciences](Academy_of_Motion_Picture_Arts_and_Sciences "wikilink")
(AMPAS), took place on March 10, 2024, at the [Dolby
Theatre](Dolby_Theatre "wikilink") in
[Hollywood](Hollywood,_Los_Angeles "wikilink"), Los Angeles.[1] During
the gala, the AMPAS presented [Academy
Awards](Academy_Awards "wikilink") (commonly referred to as Oscars) in
23 categories honoring [films released in
2023](2023_in_film "wikilink"). Comedian [Jimmy
Kimmel](Jimmy_Kimmel "wikilink") hosted the show for the fourth time.

The nominations were announced on January 23, 2024.
*[Oppenheimer](Oppenheimer_(film) "wikilink")* led with 13 nominations,
followed by *[Poor Things](Poor_Things_(film) "wikilink")* and *[Killers
of the Flower Moon](Killers_of_the_Flower_Moon_(film) "wikilink")* with
11 and 10, respectively.[2][3][4] *Oppenheimer* won a leading seven
awards, including [Best
Picture](Academy_Award_for_Best_Picture "wikilink") and [Best
Director](Academy_Award_for_Best_Director "wikilink")
[..]
```

In the taxonomy repository, here's what the previously referenced knowledge might look like in the tree:

#### Knowledge: directory tree example 

```ascii
[...]

└── knowledge
    └── textbooks
        ├── culture
        │ └── movies
        │     └── awards
        │         ├── oscars  <=== here it is :)
        │         │   └── qna.yaml
        |         |       attribution.txt
        │         └── golden_globes_movies
        │             └── qna.yaml
        |                 attribution.txt
[...]
```

You can organize the knowledge markdown files in your repository however you want. You just need to ensure the YAML is pointing to the correct file. 

## Taxonomy tree Layout

The taxonomy tree is organized in a cascading directory structure. At the end of
each branch, there is a YAML file (qna.yaml) that contains the examples for that
domain. Maintainers can decide to change the names of the existing branches or to add new branches.

> [!IMPORTANT] 
> Folder names do not have spaces. 

Below is an illustrative directory structure to show this layout:

```ascii
.
└── writing
    ├── freeform
    │   ├── brainstorming
    │   │   ├── idea_generation
    │   │   │   └── qna.yaml
    │   │   │       attribution.txt
    │   │   ├── refute_claim
    │   │   │   └── qna.yaml
    │   │   │       attribution.txt
    │   ├── prose
    │   │   ├── articles
    │   │   │   └── qna.yaml
    │   │   │       attribution.txt
    │   │   ├── emails
    │   │   │   ├── formal
    │   │   │   │   └── qna.yaml
    │   │   │   │       attribution.txt
    │   │   │   └── informal
    │   │   │       └── qna.yaml
    │   │   │           attribution.txt
    └── grounded
        ├── editing
        │   ├── grammar
        │   │   └── qna.yaml
        │   │       attribution.txt
        │   └── spelling
        │       └── qna.yaml
        │           attribution.txt
        └── summarization
            └── wiki_insights
                └── concise
                    └── qna.yaml
                        attribution.txt
```

For an extensive example of this layout see, [taxonomy_tree_layout](https://github.com/instruct-lab/taxonomy/tree/main/docs/taxonomy_tree_layout.md) in the documentation folder.

## Contribute knowledge and skills to the taxonomy!

The ability to contribute to a Large Language Model (LLM) has been difficult in no small part because it is difficult to get access to the necessary compute infrastructure.

This taxonomy repository will be used as the seed to synthesize the training data for InstructLab-trained models. We intend to retrain the model(s) using the main branch following InstructLab's progressive training on a regular basis. This enables fast iteration of the model(s), for the benefit of the open source community.

By contributing your skills and knowledge to this repository, you will see your changes built into an LLM within days of your contribution rather than months or years! If you are working with a model and notice its knowledge or ability lacking, you can correct it by contributing knowledge or skills and check if it's improved after your changes are built.

While public contributions are welcome to help drive community progress, you can also fork this repository under [the Apache License, Version 2.0](LICENSE), add your own internal skills, and train your own models internally. However, you might need your own access to significant compute infrastructure to perform sufficient retraining.

## Ways to Contribute

You can contribute to the taxonomy in the following two ways:

1. Adding new examples to **existing leaf nodes**:

    - Go to the corresponding leaf node / end of the branch and modify the YAML
    - Add a new example to the `qna.yaml` files as a new entry to the list

2. Adding **new branches/skills** corresponding to the existing domain:

    - You can add new folders under the corresponding category (replace any spaces ` ` with underscores `_`)
    - Create a new `qna.yaml` file containing examples for the new skill
  
### Detailed Contribution Instructions

#### Prerequisites

- You have a GitHub account
- You have access to this repo

#### Make a copy of the taxonomy repo

1. Go to [github.com/instruct-lab/taxonomy](https://github.com/instruct-lab/taxonomy).

2. Click **Fork** to fork your own copy of the repo.

    ![fork-button](https://github.com/instruct-lab/taxonomy/assets/799683/8487bff2-425e-483c-b27c-ef03da1c57a8)

3. On the **Create a new fork** page, enter the information into the following fields:
    - **Repository name:** `taxonomy` is fine
    - **Description:** Enter the description of _your fork_, not of the skills you will create. You can write something that makes sense to you or leave it blank.
    - **Copy the main branch only:** The box is selected by default. You can choose to leave the box selected or clear it.

4. Click **Create Fork**.

    ![Screenshot from 2024-02-28 12-41-59](https://github.com/instruct-lab/taxonomy/assets/799683/656608ef-3040-4858-96f0-9b695bea0e8f)

You will get a copy of the taxonomy repo in your github account. This is your own copy, so don't worry about making mistakes. *If you do end up making a mistake and want to start over: you can delete the fork and create a new fork.*

#### Contributing a skill

The following image shows the compositional skills directory and its contents. Skills are contributed to this directory. 

![Screenshot from 2024-02-28 12-44-05](https://github.com/instruct-lab/taxonomy/assets/799683/2038e035-5400-4848-91fb-f575db35b565)

The other top-level directory you can contribute to is the knowledge directory, which is used for knowledge contributions. You can read more about the difference between skills and knowledge in the [community documentation](https://github.com/instruct-lab/community/blob/main/docs/README.md).

Based on the directories that exist in the tree, make a best guess at where in the tree structure to add the skill that you want to contribute. If you get to a point where you've gone deep enough into the tree and you can't find any directories that match, feel free to create a new directory (and subdirectories, if needed) to best represent your skill.

For example, I want to contribute a skill for creating puns. Puns are a specific type of joke. I started in the writing directory of the tree, and saw two main directories there: freeform and grounded. 

![Screenshot from 2024-02-28 12-57-00](https://github.com/instruct-lab/taxonomy/assets/799683/2fab5b92-194a-491e-8a6f-f464a8e8f2f5)

Under the freeform directory, I saw subdirectories such as brainstorming, debate, legal, poetry, prose, etc.

![Screenshot from 2024-02-28 12-57-35](https://github.com/instruct-lab/taxonomy/assets/799683/e52ea423-d86f-49a8-9229-b09418f1510b)

Under the grounded directory, I saw subdirectories such as editing, meeting_insights, summarization/wiki_insights.

![Screenshot from 2024-02-28 12-59-10](https://github.com/instruct-lab/taxonomy/assets/799683/98370d70-d7e4-4595-a259-f6ffa4ef00fb)

Puns seemed to fit best under the freeform directory, but I didn't think they fit under any of the pre-existing directories under freeform, so I created a jokes directory. Under jokes, I created a puns subdirectory. By making jokes a directory, I can continue to add subdirectories for different types of jokes. For example, I can add a new subdirectory for the knock-knock joke skill that I want to create. 🙂

It can be a little tricky mechanically to create directories in GitHub's web UI, but you can complete the process using the following steps: 

1. In the GitHub repo, click the folder that you want to create the new directory inside of.

2. Click **Add File** and select **Create new file** from the menu.

3. Type the name of the first directory that you want to create. In the example animation, we use "jokes/" as the first directory.

> [!NOTE]
> When you type the "/" character, the directory name will "lock in" and you'll be able to type the name of the subdirectory that you want to add under it. In the example, we typed "knock-knock/" as the subdirectory name.

> [!NOTE]
> Make sure to replace any spaces (` `) in the folder name with underscores (`_`)

4. After you have entered the name of all of the directories that you want to add, type the file name. The file name should always be `qna.yaml` (qna stands for "Question aNd Answer.")

Here's an animated graphic to show how it works:

![screencast-directory-naming](https://github.com/instruct-lab/taxonomy/assets/799683/2cb2b031-52f6-46de-bfd9-c4eae82ec9d3)

**TO BE CONTINUED**

#### Contributing Knowledge
This information will be added once knowledge contributions are opened up. 

### How should I contribute?

For additional information about how to make a contribution, see the
[documentation on contributing](CONTRIBUTING.md).

### Why should I contribute?

This taxonomy repository will be used as the seed to synthesize the training
data for InstructLab-trained models. We intend to retrain the model(s) using the main
branch as often as possible (at least weekly). Fast iteration of the model(s) benefits the open source community and enables model developers who do not have access to the necessary compute infrastructure.
