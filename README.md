<!-- Improved compatibility of back to top link: See: https://github.com/othneildrew/Best-README-Template/pull/73 -->
<a name="readme-top"></a>
<!--
*** Thanks for checking out the Best-README-Template. If you have a suggestion
*** that would make this better, please fork the repo and create a pull request
*** or simply open an issue with the tag "enhancement".
*** Don't forget to give the project a star!
*** Thanks again! Now go create something AMAZING! :D
-->

<!-- PROJECT LOGO -->
<br />
<div align="center">
  <h3 align="center">Assessing LLMs' Capability to Understand TLA+</h3>

  <p align="center">
    Houming Chen, Daniel Hou, Oh Jun Kweon
  </p>
</div>


<!-- TABLE OF CONTENTS -->
<!-- <details>
  <summary>Table of Contents</summary>
  <ol>
    <li><a href="#about-the-project">About The Project</a></li>
    <li><a href="#directory-structure">Directory Structure</a></li>
    <li><a href="#usage">Usage</a></li>
  </ol>
</details> -->


<!-- ABOUT THE PROJECT -->
## About The Project

TLA+ is a formal specification language used in system engineering to design and verify protocols. We are interested in investigating how LLMs can aid TLA+ coding. To evaluate the effectiveness of various LLMs in performing TLA+ tasks, we construct two benchmarks:
<ol>
    <li>
        <b>Protocol-Identification Benchmark</b>
        <br>
        Given a TLA+ spec, can an LLM identify the protcol being implemented?
    </li>
    <li>
        <b>Bug-Identification Benchmark</b>
        <br>
        Given a buggy TLA+ spec and the name of the protocol being implemented, can an LLM:
        <ol>
            <li>identify that the spec contains a bug?</li>
            <li>explain what the bug is?</li>
        </ol>
    </li>
</ol>


<!-- Directory Structure -->
## Directory Structure

Note: all correct TLA+ specs used in this project are sourced from [https://github.com/tlaplus/Examples](https://github.com/tlaplus/Examples).

Directory Structure:
<ul>
  <li>mutation-identification-benchmark</li>
  <ul>
    <li>correct_specs</li>
    <ul>
      <li>2pc_correct.txt</li>
      <li>paxos_correct.txt</li>
      <li>raft_correct.txt</li>
    </ul>
    <li>mutations</li>
    <ul>
      <li>2pc</li>
      <li>paxos</li>
      <li>raft</li>
    </ul>
  </ul>
  <li>protocol-identification-benchmark</li>
  <ul>
    <li>...list of protocols with correct TLA+ specs...</li>
  </ul>
</ul>

The interesting files are in mutation-identification-benchmark/mutations/{protocol}.
For a given protocol, the directory contains:
<ul>
  <li>gpt3.5</li>
  <li>gpt4</li>
  <li>llama2</li>
  <li>palm</li>
  <li>main.py</li>
  <li>{protocol}_mod_explanations.txt</li>
  <li>results_summary_{protocol}.txt</li>
  <li>{protocol}_mod_{i}.txt (for i in [1:10])</li>
</ul>

In each model directory (gpt3.5, gpt4, llama2, palm), you will find model responses to all 10 mutations run 4 times each.

In main.py, you will find the script we wrote to automatically run the benchmark on all models. More information on how to use this can be found in the [Usage](#usage) section below.

In {protocol}_mod_explanations.txt, you will find a natural language explanation of the bugs introduced in each mutation, and the lines of code affected.

In results_summary_{protocol}.txt, you will find the accuracy of each model on each run of each mutation of each protocol.

In {protocol}_mod_{i}.txt (for i in [1:10]), you will find the actual buggy TLA+ spec that we input to each model.


<!-- USAGE -->
## Usage

[Directory Structure](#directory-structure) explains how to find the main.py file for each protocol. This section explains how to use main.py. Note that additional usage information can be found at the top of the main.py file itself.

'''
python3 main.py {model}
'''
where model is one of gpt3.5, gpt4, llama2, palm, or bard.

text