# ECE250 Testcases

This repository contains a collection of MIT-licensed testcases for each project in ECE250.

| Project | Number Of Testcases Available |
|---------|-------------------------------|
| Project 1 | 23 (22 active in manifest) |
| Project 2 | 34 (34 active in manifest) |
| Project 3 | 31 (30 active in manifest) |
| Project 4 | 9 (9 active in manifest) + 8 datasets |


# Sweet, but how do I use them?

Follow through the instructions in the "Setup" section, then actually test your project by following the "Automatic Testing" section.

## Setup

As recommended time and time again by the teaching staff, it is highly recommended you do your testing from an eceubuntu server.
Steps to connect to such a server are beyond the scope of this README.

Once you're logged into an eceubuntu server (or a local Unix/Linux system of your own), clone this repository:

```
$ git clone https://github.com/JZJisawesome/ece250-testcases
Cloning into 'ece250-testcases'...
remote: Enumerating objects: 738, done.
remote: Counting objects: 100% (302/302), done.
remote: Compressing objects: 100% (217/217), done.
remote: Total 738 (delta 134), reused 208 (delta 78), pack-reused 436
Receiving objects: 100% (738/738), 644.47 KiB | 3.08 MiB/s, done.
Resolving deltas: 100% (366/366), done.
```

If you already have a checkout but want to get the latest testcases and AutoGrader fixes, you can do this instead (from within your previous clone):

```
$ git pull
remote: Enumerating objects: 246, done.
remote: Counting objects: 100% (245/245), done.
remote: Compressing objects: 100% (164/164), done.
remote: Total 235 (delta 116), reused 169 (delta 66), pack-reused 0
Receiving objects: 100% (235/235), 99.48 KiB | 1.36 MiB/s, done.
Resolving deltas: 100% (116/116), completed with 5 local objects.
From https://github.com/JZJisawesome/ece250-testcases
   8820b46..0e35dfb  main       -> origin/main
[...]
```

## Automatic Testing

The autograder implementation included in this repo, called the Jekel AutoGrader, **must be run from the repo root directory**.
Note down the path to your submission tarball, and open a terminal **in the root of the repo**. You can then test your tarball with

```
$ python3 ./jekelautograder.py path/to/your/tarball/example_p1.tar.gz
     _      _        _      _         _         ____               _
    | | ___| | _____| |    / \  _   _| |_ ___  / ___|_ __ __ _  __| | ___ _ __
 _  | |/ _ \ |/ / _ \ |   / _ \| | | | __/ _ \| |  _| '__/ _` |/ _` |/ _ \ '__|
| |_| |  __/   <  __/ |  / ___ \ |_| | || (_) | |_| | | | (_| | (_| |  __/ |
 \___/ \___|_|\_\___|_| /_/   \_\__,_|\__\___/ \____|_|  \__,_|\__,_|\___|_|    for ECE 250
Copyright (c) 2023 John Jekel, Aiden Fox Ivey, and ECE 250 Teaching Staff

Performing some basic sanity checks before we get started...
Looking good, I think I'm set to go!

To begin, let's check your tarball's file name and path...
Excellent! Based on the name of the tarball, example_p1.tar.gz, I've deduced the following:
Your UWID is: example
Your tarball is for: Project 1
[...]
```

The autograder will then test your tarball not only on the testcases for the correct project, but it will also check some other things:

- That the tarball is named correctly (it must be in order for the script to successfully infer the project version)
- That your design document is present and named correctly (matches the uwid in your tarball's name, etc.)
- That your Makefile is present and successfully produces an a.out file
- That you didn't accidentally include a precompiled a.out file in your tarball
- That your tarball dosn't contain any directories

Just like the real thing, the autograder will use Valgrind, so it is quite good at catching mistakes!

(It uses Leaks on MacOS)

## Manual Testing

This is useful if you are debugging an issue with your code that is triggered by a particular test case

The projects/ folder contains several subdirectories, one for each project.
Within the project folder you're interested in, there is an "input" and an "output" folder.

Each file in "input" is a testcase you can run with the following command (assuming you have
Valgrind installed and your code is compiled to the binary a.out)

```
$ valgrind ./a.out < path/to/testcase.in
[...]
```

You can then compare the results to the corresponding file in the "output" folder to ensure your program produces the correct output!

TODO instructions for manual testing with Leaks

# Testcase Descriptions

## Project 3

| Testcase | Description |
|----------|-------------|
| alphabetic_print | Loads the corpus and prints it. A good way to check your are printing correctly in alphabetical order. |
| can_you_count | Testcase to test the count prefix command. |
| chatgpt_autogenerated_{0, 1, 2} | These are testcases autogenerated by ChatGPT, with some manual fixes. They can be hit or miss with regards to their utility in debugging/testing. |
| dont_erase_too_much | Erases words and ensures you don't accidentally erase other ones by mistake. Also makes sure your size variable remains consistent with the number of words present. |
| double_erase | Erases a word twice and ensures the behaviour is as expected |
| erasing_clear | Loads the corpus and clears it, then prints, inserts and removes to the empty trie. |
| illegal_erase | Attempt to erase a word with both valid and invalid characters to ensure the valid characters stay unerased |
| illegal_insert | Input a word with both valid and invalid characters to ensure the valid letters are not inserted |
| illegal_prefix | Input a prefix with both valid and invalid characters to ensure prefixes are counted properly and error messages are prioritized |
| insanity | JZJ's classic insanity test. This is the biggest one yet (almost 1 MB), but it shouldn't take that long since the trie is pretty efficient as data structures go! |
| im_empty_inside | Tests to ensure commands work properly when the trie is empty. |
| invalid | Tests how you handle invalid input for i, c, and e. |
| LEARN_test0{1, 2, 3, 4} | Tests provided by the ECE 250 Teaching Staff (from LEARN). |
| long_words | Tests words that are much longer than normal. |
| more_spellchecking | A few additional spellcheck commands I sort of accidentally came up with while trying to create spellcheck_no_suggestions. |
| multiload | Performs multiple loads and clears, using empty and size to ensure everything worked |
| nested_erase | Inserts a word and another word embedded in the previous word and erases both words. |
| prefix_example_from_spec | Tests the example situation mentioned in the spec on LEARN, with CAR, CARD, and CARMEN. |
| prefix_peril | Tries the "c" command in a bunch of situations, trying to invoke edgecases (ex. no prefixes available, the prefix is a valid word, the prefix is near the root, etc). |
| sanity | JZJ's classic sanity test. Just a single line: "exit" |
| single_letters | A testcase that inserts, removes, and prints several words that are only 1 letter long. |
| spellcheck_correct | Loads the corpus, and spellchecks every word, which should print "correct" each time. |
| spellcheck_example_from_spec | Tests the example situation mentioned in the spec on LEARN, with YOU, YOUN, YOUNG, and YOUR. |
| spellcheck_no_suggestions | Loads the corpus, and spellchecks several wrong words that have no suggestions. This is an edge case: newlines should be printed, **not all of the words**. |
| spellcheck_incorrect | Loads the corpus, and spellchecks several wrong words, trying to cover several edge cases when searching for suggestions. |
| YodaErase | A small testcase that ensure things still work, even with entirely unique words. |

## Project 4

| Testcase | Description |
|----------|-------------|
| fm_01 | Loads the graph example from Chapter 23 of CLRS. A standard check for the MST and cost calculations. |
| im_empty_inside_again | Tests to ensure your graph behaves well when it is empty |
| integer_limits | Tests to ensure your code can handle input near the signed integer limits |
| invalid | Tests to ensure your code correctly rejects invalid vertex numbers and weights |
| LEARN_{smallGraph, testFull} | Tests provided by the ECE 250 Teaching Staff (from LEARN). Note LEARN_testFull uses the LEARN_bigGraph dataset. |
| sanity | JZJ's classic sanity test. Just a single line: "END" |
| starburst | Loads the starburst.in dataset and deletes the center of the star. This causes 1000 verticies to be removed with a single command. |
| vertex_weight_limits | Tests to ensure your code works correctly even when vertex numbers and weights are near their minimums and maximums. |

| Dataset | Description |
|---------|-------------|
| empty.in | The dataset with no edges in it |
| fm_CLRS_example.in | The graph example from Chapter 23 of CLRS, used by the fm_01 testcase. |
| LEARN_bigGraph.in | Dataset provided by the ECE 250 Teaching Staff (from LEARN). |
| jzj_standard_{big, insanity, medium, normal, tiny}.in | JZJ's standard datasets (of various sizes) used by his testcases (and free for others to use for their testcases too!) |
| starburst.in | The dataset for the starburst testcase. A single vertex is connected to 999 others through 999 edges. These are the only edges in the whole graph. |

# Contributing

By having your testcases included in this repository, you agree to having them released under the MIT License (of course you retain copyright).
You'll get a spot in the following "Contributors" section of the README for your contributions, indicating which test files are yours.

Only input files with a corresponding expected output file will be accepted for inclusion. Furthermore, as of Project 3, you must also provide a description of your testcase (and datasets) in this README.

Just **submit a PR** to participate, or if you're a big enough contributor, I'll grant you maintainer status :)

# Contributors

## Jekel AutoGrader

| Contributor |
|-------------|
| Aiden Fox Ivey |
| ECE 250 Teaching Staff |
| John Jekel |

## Project 1

| Contributor | Number Of Testcases Contributed | Testcase Names |
|-------------|---------------------------------|----------------|
| AlexanderTsarapkine | 1 | edge_cases_mem_leak |
| Azizul Chowdhury | 1 | test_REM |
| ChatGPT (with manual fixes) | 3 | chatgpt_autogenerated_0, chatgpt_autogenerated_1, chatgpt_autogenerated_2 |
| Chris (HyperFire12#3764) | 1 | specificboy |
| ECE 250 Teaching Staff | 3 | LEARN_test01, LEARN_test02, LEARN_test03 |
| Farzan Mirshekari | 3 | ECE250-Projects-Testcases_test04, ECE250-Projects-Testcases_test05, ECE250-Projects-Testcases_test06 |
| Hongjun Yun | 1 | hongjun_total_testing |
| John Jekel (JZJ) | 6 | insanity, list_size_1, pushpop_yum, sanity, supports_double, support_valid_cpp_names |
| Luc Edes | 1 | delete |
| Nathan Cheng | 1 | edge_cases |
| Nick Chan | 1 | doingstuff |
| Tri Dao | 1 | test_DEF |

## Project 2

| Contributor | Number Of Testcases Contributed | Testcase Names |
|-------------|---------------------------------|----------------|
| AndyGolow | 9 | ag_testcase_01, ag_testcase_02, ag_testcase_03, ag_testcase_04, ag_testcase_05, ag_testcase_06, ag_testcase_07, ag_testcase_09, ag_testcase_10 |
| ChatGPT (with manual fixes) | 3 | chatgpt_autogenerated_0, chatgpt_autogenerated_1, chatgpt_autogenerated_2 |
| ECE 250 Teaching Staff | 4 | LEARN_test01open, LEARN_test01ordered, LEARN_test02ordered, LEARN_test03ordered |
| Farzan Mirshekari | 2 | ECE250-Projects-Testcases_test02open, ECE250-Projects-Testcases_test03open |
| John Jekel (JZJ) | 13 | insanity_open, insanity_ordered, integer_limits_open, integer_limits_ordered, oob_open, oob_ordered, printer, respect_capacity_open, respect_capacity_ordered, respect_capacity1_open, respect_capacity1_ordered, sanity_open, sanity_ordered |
| Nick Chan | 1 | nc_open01 |
| Reezan Visram | 1 | ECE250-Projects-Testcases_test04ordered |
| Ryan (RyEggGit) | 1 | linkingtest |
| Mihir | 1 | integer_limits_open_for_integers, integer_limits_ordered_for_integers |

## Project 3

| Contributor | Number Of Testcases Contributed | Testcase Names |
|-------------|---------------------------------|----------------|
| Adam Goldman | 1 | single_letters |
| Brandon Vo | 3 | illegal_erase, illegal_insert, illegal_prefix |
| Chimera | 1 | YodaErase |
| ChatGPT (with manual fixes) | 3 | chatgpt_autogenerated_0, chatgpt_autogenerated_1, chatgpt_autogenerated_2 |
| ECE 250 Teaching Staff | 4 | LEARN_test01, LEARN_test01, LEARN_test02, LEARN_test03 |
| John Jekel (JZJ) | 15 | alphabetic_print, dont_erase_too_much, im_empty_inside, insanity, invalid, long_words, more_spellchecking, multiload, prefix_example_from_spec, prefix_peril, sanity, spellcheck_correct, spellcheck_example_from_spec, spellcheck_no_suggestions, spellcheck_incorrect |
| Josh Quittner | 1 | erasing_clear |
| Mihir | 2 | double_erase, nested_erase |
| Nick Chan | 1 | can_you_count |

## Project 4

| Contributor | Number Of Testcases Contributed | Testcase Names | Number of Datasets Contributed | Dataset Names |
|-------------|---------------------------------|----------------|--------------------------------|---------------|
| ECE 250 Teaching Staff | 2 | LEARN_smallGraph, LEARN_testFull | 1 | LEARN_bigGraph.in |
| Farzan Mirshekari | 1 | fm_01 | 1 | fm_CLRS_example.in |
| John Jekel (JZJ) | 6 | im_empty_inside_again, integer_limits, invalid, sanity, starburst, vertex_weight_limits | 7 | empty.in, jzj_standard_big.in, jzj_standard_insanity.in, jzj_standard_medium.in, jzj_standard_normal.in, jzj_standard_tiny.in, starburst.in |
