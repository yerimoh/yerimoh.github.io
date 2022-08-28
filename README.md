# Moon Jekyll Theme [![Donate](https://img.shields.io/badge/paypal-donate-blue.svg)](https://www.paypal.me/taylantatli/0usd)  
   
## `Sorry guys but there will be no update until I buy a new laptop.`
    
######(If you like this theme or using it, please give a :star: for motivation.)

**[Moon](https://taylantatli.github.io/Moon)** is a minimal, one column jekyll theme.



Model Variations
To evaluate the importance of different components of the Transformer, we varied our base model
in different ways, measuring the change in performance on English-to-German translation on the
development set, newstest2013. We used beam search as described in the previous section, but no
checkpoint averaging. We present these results in Table 3.
In Table 3 rows (A), we vary the number of attention heads and the attention key and value dimensions,
keeping the amount of computation constant, as described in Section 3.2.2. While single-head
attention is 0.9 BLEU worse than the best setting, quality also drops off with too many heads.
5We used values of 2.8, 3.7, 6.0 and 9.5 TFLOPS for K80, K40, M40 and P100, respectively.
8
Table 3: Variations on the Transformer architecture. Unlisted values are identical to those of the base
model. All metrics are on the English-to-German translation development set, newstest2013. Listed
perplexities are per-wordpiece, according to our byte-pair encoding, and should not be compared to
per-word perplexities.

## Features 
* Minimal, you can focus on your content 
* Responsive  
* Disqus integration
* Syntax highlighting
* Optional post image
* Social icons
* Page for sharing projects
* Optional background image
* Simple navigation menu
* MathJax support 
 
## Preview

![screenshot of Moon](https://cloud.githubusercontent.com/assets/754514/14509720/61c61058-01d6-11e6-93ab-0918515ecd56.png)    
![screenshot of Moon](https://cloud.githubusercontent.com/assets/754514/14509716/61ac6c8e-01d6-11e6-879f-8308883de790.png)

See a [live version of Moon](https://taylantatli.github.io/Moon) hosted on GitHub.

## Getting Started

To learn how to install and use this theme check out the [Setup Guide](https://taylantatli.github.io/Moon/moon-theme/) for more information.
