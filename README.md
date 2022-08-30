# NCBI-DISEASE-CLASSIFIER

Disease word classifier model comparison with different types of neural networks (CNN, GRU, LSTM) using [ncbi_disease dataset](https://huggingface.co/datasets/ncbi_disease). This data was retrieved from Hugging face dataset api. The project aims to apply named entity recognition on disease names.

## Dataset Preview

<table class="table-auto rounded-lg font-mono w-full text-gray-900 text-xs"><thead class="sticky top-0 left-0 right-0 bg-white shadow-sm z-10"><tr class="border-b text-left divide-x dark:divide-gray-800 space-y-54"><th class="max-w-sm p-2 text-left">id (string)</th><th class="max-w-sm p-2 text-left">tokens (json)</th><th class="max-w-sm p-2 text-left">ner_tags (json)</th></tr></thead>
    <tbody class="h-16 overflow-scroll"><tr class="border-b last:border-none divide-x dark:divide-gray-800 space-x-4 odd:bg-gray-50 dark:odd:bg-gray-900 group hover:cursor-pointer focus:bg-gradient-to-b focus:from-blue-100 dark:focus:from-blue-900 focus:to-blue-50 dark:focus:to-gray-900 hover:bg-gray-100 dark:hover:bg-gray-900 focus:odd:bg-white" tabindex="0"><td class="max-w-sm break-words p-2 group-focus:align-top"><div class="line-clamp-2 group-focus:line-clamp-none">
<div class="" dir="auto">0
</div></div>
                    </td><td class="max-w-sm break-words p-2 group-focus:align-top"><div class="line-clamp-2 group-focus:line-clamp-none">
<div class="" dir="auto">[
"Identification",
"of",
"APC2",
",",
"a",
"homologue",
"of",
"the",
"adenomatous",
"polyposis",
"coli",
"tumour",
"suppressor",
"."
]
</div></div>
                    </td><td class="max-w-sm break-words p-2 group-focus:align-top"><div class="line-clamp-2 group-focus:line-clamp-none">
<div class="" dir="auto">[
0,
0,
0,
0,
0,
0,
0,
0,
1,
2,
2,
2,
0,
0
]
</div></div>
                    </td>
            </tr><tr class="border-b last:border-none divide-x dark:divide-gray-800 space-x-4 odd:bg-gray-50 dark:odd:bg-gray-900 group hover:cursor-pointer focus:bg-gradient-to-b focus:from-blue-100 dark:focus:from-blue-900 focus:to-blue-50 dark:focus:to-gray-900 hover:bg-gray-100 dark:hover:bg-gray-900 focus:odd:bg-white" tabindex="0"><td class="max-w-sm break-words p-2 group-focus:align-top"><div class="line-clamp-2 group-focus:line-clamp-none">
<div class="" dir="auto">1
</div></div>
                    </td><td class="max-w-sm break-words p-2 group-focus:align-top"><div class="line-clamp-2 group-focus:line-clamp-none">
<div class="" dir="auto">[
"The",
"adenomatous",
"polyposis",
"coli",
"(",
"APC",
")",
"tumour",
"-",
"suppressor",
"protein",
"controls",
"the",
"Wnt",
"signalling",
"pathway",
"by",
"forming",
"a",
"complex",
"with",
"glycogen",
"synthase",
"kinase",
"3beta",
"(",
"GSK",
"-",
"3beta",
")",
",",
"axin",
"/",
"conductin",
"and",
"betacatenin",
"."
]
</div></div>
                    </td><td class="max-w-sm break-words p-2 group-focus:align-top"><div class="line-clamp-2 group-focus:line-clamp-none">
<div class="" dir="auto">[
0,
1,
2,
2,
2,
2,
2,
2,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0
]
</div></div>
                    </td>
            </tr><tr class="border-b last:border-none divide-x dark:divide-gray-800 space-x-4 odd:bg-gray-50 dark:odd:bg-gray-900 group hover:cursor-pointer focus:bg-gradient-to-b focus:from-blue-100 dark:focus:from-blue-900 focus:to-blue-50 dark:focus:to-gray-900 hover:bg-gray-100 dark:hover:bg-gray-900 focus:odd:bg-white" tabindex="0"><td class="max-w-sm break-words p-2 group-focus:align-top"><div class="line-clamp-2 group-focus:line-clamp-none">
<div class="" dir="auto">2
</div></div>
                    </td><td class="max-w-sm break-words p-2 group-focus:align-top"><div class="line-clamp-2 group-focus:line-clamp-none">
<div class="" dir="auto">[
"Complex",
"formation",
"induces",
"the",
"rapid",
"degradation",
"of",
"betacatenin",
"."
]
</div></div>
                    </td><td class="max-w-sm break-words p-2 group-focus:align-top"><div class="line-clamp-2 group-focus:line-clamp-none">
<div class="" dir="auto">[
0,
0,
0,
0,
0,
0,
0,
0,
0
]
</div></div>
                    </td>
            </tr><tr class="border-b last:border-none divide-x dark:divide-gray-800 space-x-4 odd:bg-gray-50 dark:odd:bg-gray-900 group hover:cursor-pointer focus:bg-gradient-to-b focus:from-blue-100 dark:focus:from-blue-900 focus:to-blue-50 dark:focus:to-gray-900 hover:bg-gray-100 dark:hover:bg-gray-900 focus:odd:bg-white" tabindex="0"><td class="max-w-sm break-words p-2 group-focus:align-top"><div class="line-clamp-2 group-focus:line-clamp-none">
<div class="" dir="auto">3
</div></div>
                    </td><td class="max-w-sm break-words p-2 group-focus:align-top"><div class="line-clamp-2 group-focus:line-clamp-none">
<div class="" dir="auto">[
"In",
"colon",
"carcinoma",
"cells",
",",
"loss",
"of",
"APC",
"leads",
"to",
"the",
"accumulation",
"of",
"betacatenin",
"in",
"the",
"nucleus",
",",
"where",
"it",
"binds",
"to",
"and",
"activates",
"the",
"Tcf",
"-",
"4",
"transcription",
"factor",
"(",
"reviewed",
"in",
"[",
"1",
"]",
"[",
"2",
"]",
")",
"."
]
</div></div>
                    </td><td class="max-w-sm break-words p-2 group-focus:align-top"><div class="line-clamp-2 group-focus:line-clamp-none">
<div class="" dir="auto">[
0,
1,
2,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0
]
</div></div>
                    </td>
            </tr><tr class="border-b last:border-none divide-x dark:divide-gray-800 space-x-4 odd:bg-gray-50 dark:odd:bg-gray-900 group hover:cursor-pointer focus:bg-gradient-to-b focus:from-blue-100 dark:focus:from-blue-900 focus:to-blue-50 dark:focus:to-gray-900 hover:bg-gray-100 dark:hover:bg-gray-900 focus:odd:bg-white" tabindex="0"><td class="max-w-sm break-words p-2 group-focus:align-top"><div class="line-clamp-2 group-focus:line-clamp-none">
<div class="" dir="auto">4
</div></div>
                    </td><td class="max-w-sm break-words p-2 group-focus:align-top"><div class="line-clamp-2 group-focus:line-clamp-none">
<div class="" dir="auto">[
"Here",
",",
"we",
"report",
"the",
"identification",
"and",
"genomic",
"structure",
"of",
"APC",
"homologues",
"."
]
</div></div>
                    </td><td class="max-w-sm break-words p-2 group-focus:align-top"><div class="line-clamp-2 group-focus:line-clamp-none">
<div class="" dir="auto">[
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0
]
</div></div>
                    </td>
            </tr><tr class="border-b last:border-none divide-x dark:divide-gray-800 space-x-4 odd:bg-gray-50 dark:odd:bg-gray-900 group hover:cursor-pointer focus:bg-gradient-to-b focus:from-blue-100 dark:focus:from-blue-900 focus:to-blue-50 dark:focus:to-gray-900 hover:bg-gray-100 dark:hover:bg-gray-900 focus:odd:bg-white" tabindex="0"><td class="max-w-sm break-words p-2 group-focus:align-top"><div class="line-clamp-2 group-focus:line-clamp-none">
<div class="" dir="auto">5
</div></div>
                    </td><td class="max-w-sm break-words p-2 group-focus:align-top"><div class="line-clamp-2 group-focus:line-clamp-none">
<div class="" dir="auto">[
"Mammalian",
"APC2",
",",
"which",
"closely",
"resembles",
"APC",
"in",
"overall",
"domain",
"structure",
",",
"was",
"functionally",
"analyzed",
"and",
"shown",
"to",
"contain",
"two",
"SAMP",
"domains",
",",
"both",
"of",
"which",
"are",
"required",
"for",
"binding",
"to",
"conductin",
"."
]
</div></div>
                    </td><td class="max-w-sm break-words p-2 group-focus:align-top"><div class="line-clamp-2 group-focus:line-clamp-none">
<div class="" dir="auto">[
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0,
0
]
</div></div>
                    </td>
            </tr></tbody></table>

<br>

# Dataset Structure

### Data Instances

Instances of the dataset contain an array of `tokens`, `ner_tags` and an `id`.

Sample data from the dataset:

```
{
  'tokens': ['Identification', 'of', 'APC2', ',', 'a', 'homologue', 'of', 'the', 'adenomatous', 'polyposis', 'coli', 'tumour', 'suppressor', '.'],
  'ner_tags': [0, 0, 0, 0, 0, 0, 0, 0, 1, 2, 2, 2, 0, 0],
  'id': '0'
}
```

### Data Fields

- `id`: Sentence identifier.
- `tokens`: Array of tokens composing a sentence.
- `ner_tags`: Array of tags, where `0` indicates no disease mentioned, `1` signals the first token of a disease and `2` the subsequent disease tokens.

[For more detailed information about dataset](https://huggingface.co/datasets/ncbi_disease)

<br>

# Preprocessing

### Removing Stopwords and Punctuations

The data above had some punctuation chars and stopwords inside **tokens** column. These elements and their corresponding tags have been removed for a clean result and no unwanted classifications.

### Words to Sequences and Sequence Padding

The data is vectorized in order to be sequenced and padded via tokenizer. Since CNN only accepts fixed size data, the lengths of all sentences are made the same size.

<br>

# Model Training

Since our problem is basically a multi class classification problem all of the output layers use "softmax" as an activation function. Also for each model "sparse categorical corssentropy" loss function is used.

## Only Embedding Model

After some experiment it is observed that the model is tend to overfit. For this reason dropout layer has been used with a probability 0.6. Also the learning rate has been setted to 0.0005.

## CNN Model

On this model only single 1d convolutional layer has been used. Filters are defined as 16 and kernel size defined as 2. Same as previous model this model is tend to overfit. Therefore before the output layer dropout layer has been used.

## GRU Model

All of the RNN based models (GRU, LSTM, Multiple LSTM) have bidirectional layer in this experiment. Basic GRU model with 32 unit. Only advantage of this model it is more easy to train than basic LSTM cells.

## LSTM

This model has better results than the GRU model but it's training duration is more than the GRU model.

## Multiple LSTM

Due to not enough data this model is the most overfitted model in the experiment. In spite of dropout layer and low learning rate. Also takes the longest to train.

# Evaluation

The accuracy and loss values on the test data are listed below.

```
test loss, test acc: [0.2331709861755371, 0.9312196969985962]  <->  Only Embedding

test loss, test acc: [0.2950023710727691, 0.8634837865829468]  <->  CNN

test loss, test acc: [0.2362357676029205, 0.9317418932914734]  <->  GRU

test loss, test acc: [0.2362425923347473, 0.9315180778503418]  <->  Bidi LSTM

test loss, test acc: [0.2752841413021087, 0.8601267933845526]  <->  Multiple Bidi LSTM
```
