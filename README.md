Download Link: https://assignmentchef.com/product/solved-sentiment-analysis-cs221-hw2
<br>
Advice for this homework:

<ol class="problem">

 <li>Words are simply strings separated by whitespace. Note that words which only differ in capitalization are considered seperate (e.g. <i>great</i> and <i>Great</i> are unique words).</li>

 <li>You might find some useful functions in <code><a href="util.py">util.py</a></code>. Have a look around in there before you start coding.</li>

</ol>

Here are two reviews of <i>Frozen</i>, courtesy of <a href="https://www.rottentomatoes.com">Rotten Tomatoes</a> (no spoilers!):

<img decoding="async" data-src="posreview.jpg" class="lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

 <noscript>

  <img decoding="async" src="posreview.jpg">

 </noscript> <img decoding="async" data-src="negreview.jpg" class="lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

 <noscript>

  <img decoding="async" src="negreview.jpg">

 </noscript>

Rotten Tomatoes has classified these reviews as “positive” and “negative,”, respectively, as indicated by the intact tomato on the left and the splattered tomato on the right. In this assignment, you will create a simple text classification system that can perform this task automatically.

<ol class="problem">

 <li style="list-style-type: none;">

  <ol class="problem">

   We’ll warm up with the following set of four mini-reviews, each labeled positive (

  </ol></li>

</ol>

<span id="MathJax-Element-1-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-1" class="math"><span id="MathJax-Span-2" class="mrow"><span id="MathJax-Span-3" class="mo">+</span><span id="MathJax-Span-4" class="mn">1</span></span></span></span>

<ol class="problem">

 <li style="list-style-type: none;">

  <ol class="problem">

   ) or negative (

  </ol></li>

</ol>

<span id="MathJax-Element-2-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-5" class="math"><span id="MathJax-Span-6" class="mrow"><span id="MathJax-Span-7" class="mo">−</span><span id="MathJax-Span-8" class="mn">1</span></span></span></span>

<ol class="problem">

 <li style="list-style-type: none;">

  <ol class="problem">

   ):




   <li style="list-style-type: none;">

    <ol>

     <li>(<span id="MathJax-Element-3-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-9" class="math"><span id="MathJax-Span-10" class="mrow"><span id="MathJax-Span-11" class="mo">−</span><span id="MathJax-Span-12" class="mn">1</span></span></span></span>) pretty bad</li>

     <li>(<span id="MathJax-Element-4-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-13" class="math"><span id="MathJax-Span-14" class="mrow"><span id="MathJax-Span-15" class="mo">+</span><span id="MathJax-Span-16" class="mn">1</span></span></span></span>) good plot</li>

     <li>(<span id="MathJax-Element-5-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-17" class="math"><span id="MathJax-Span-18" class="mrow"><span id="MathJax-Span-19" class="mo">−</span><span id="MathJax-Span-20" class="mn">1</span></span></span></span>) not good</li>

     <li>(<span id="MathJax-Element-6-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-21" class="math"><span id="MathJax-Span-22" class="mrow"><span id="MathJax-Span-23" class="mo">+</span><span id="MathJax-Span-24" class="mn">1</span></span></span></span>) pretty scenery</li>

    </ol></li>

   Each review

  </ol></li>

</ol>

<span id="MathJax-Element-7-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-25" class="math"><span id="MathJax-Span-26" class="mrow"><span id="MathJax-Span-27" class="mi">x</span></span></span></span>

<ol class="problem">

 <li style="list-style-type: none;">

  <ol class="problem">

    is mapped onto a feature vector

  </ol></li>

</ol>

<span id="MathJax-Element-8-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-28" class="math"><span id="MathJax-Span-29" class="mrow"><span id="MathJax-Span-30" class="mi">ϕ</span><span id="MathJax-Span-31" class="mo">(</span><span id="MathJax-Span-32" class="mi">x</span><span id="MathJax-Span-33" class="mo">)</span></span></span></span>

<ol class="problem">

 <li style="list-style-type: none;">

  <ol class="problem">

   , which maps each word to the number of occurrences of that word in the review. For example, the first review maps to the (sparse) feature vector

  </ol></li>

</ol>

<span id="MathJax-Element-9-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-34" class="math"><span id="MathJax-Span-35" class="mrow"><span id="MathJax-Span-36" class="mi">ϕ</span><span id="MathJax-Span-37" class="mo">(</span><span id="MathJax-Span-38" class="mi">x</span><span id="MathJax-Span-39" class="mo">)</span><span id="MathJax-Span-40" class="mo">=</span><span id="MathJax-Span-41" class="mo">{</span><span id="MathJax-Span-42" class="mtext">pretty</span><span id="MathJax-Span-43" class="mo">:</span><span id="MathJax-Span-44" class="mn">1</span><span id="MathJax-Span-45" class="mo">,</span><span id="MathJax-Span-46" class="mtext">bad</span><span id="MathJax-Span-47" class="mo">:</span><span id="MathJax-Span-48" class="mn">1</span><span id="MathJax-Span-49" class="mo">}</span></span></span></span>

<ol class="problem">

 <li style="list-style-type: none;">

  <ol class="problem">

   . Recall the definition of the hinge loss:

  </ol></li>

</ol>

<ol class="problem">

 <li style="list-style-type: none;">

  <ol class="problem">

   where

  </ol></li>

</ol>

<span id="MathJax-Element-11-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-84" class="math"><span id="MathJax-Span-85" class="mrow"><span id="MathJax-Span-86" class="mi">y</span></span></span></span>

<ol class="problem">

  is the correct label.




 <li id="1a" class="writeup">[2 points] Suppose we run stochastic gradient descent, updating the weights according toonce for each of the four examples in order. After the classifier is trained on the given four data points, what are the weights of the six words (“pretty”, “good”, “bad”, “plot”, “not”, “scenery”) that appear in the above reviews? Use <span id="MathJax-Element-13-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-118" class="math"><span id="MathJax-Span-119" class="mrow"><span id="MathJax-Span-120" class="mi">η</span><span id="MathJax-Span-121" class="mo">=</span><span id="MathJax-Span-122" class="mn">1</span></span></span></span> as the step size and initialize <span id="MathJax-Element-14-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-123" class="math"><span id="MathJax-Span-124" class="mrow"><span id="MathJax-Span-125" class="texatom"><span id="MathJax-Span-126" class="mrow"><span id="MathJax-Span-127" class="mi">w</span></span></span><span id="MathJax-Span-128" class="mo">=</span><span id="MathJax-Span-129" class="mo">[</span><span id="MathJax-Span-130" class="mn">0</span><span id="MathJax-Span-131" class="mo">,</span><span id="MathJax-Span-132" class="mo">.</span><span id="MathJax-Span-133" class="mo">.</span><span id="MathJax-Span-134" class="mo">.</span><span id="MathJax-Span-135" class="mo">,</span><span id="MathJax-Span-136" class="mn">0</span><span id="MathJax-Span-137" class="mo">]</span></span></span></span>. Assume that <span id="MathJax-Element-15-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-138" class="math"><span id="MathJax-Span-139" class="mrow"><span id="MathJax-Span-140" class="msubsup"><span id="MathJax-Span-141" class="mi">∇</span><span id="MathJax-Span-142" class="texatom"><span id="MathJax-Span-143" class="mrow"><span id="MathJax-Span-144" class="mi">w</span></span></span></span><span id="MathJax-Span-145" class="msubsup"><span id="MathJax-Span-146" class="mtext">Loss</span><span id="MathJax-Span-147" class="texatom"><span id="MathJax-Span-148" class="mrow"><span id="MathJax-Span-149" class="mtext">hinge</span></span></span></span><span id="MathJax-Span-150" class="mo">(</span><span id="MathJax-Span-151" class="mi">x</span><span id="MathJax-Span-152" class="mo">,</span><span id="MathJax-Span-153" class="mi">y</span><span id="MathJax-Span-154" class="mo">,</span><span id="MathJax-Span-155" class="texatom"><span id="MathJax-Span-156" class="mrow"><span id="MathJax-Span-157" class="mi">w</span></span></span><span id="MathJax-Span-158" class="mo">)</span><span id="MathJax-Span-159" class="mo">=</span><span id="MathJax-Span-160" class="mn">0</span></span></span></span> when the margin is exactly 1.</li>

 <li id="1b" class="writeup">[2 points] Create a small labeled dataset of four mini-reviews using the words “not”, “good”, and “bad”, where the labels make intuitive sense. Each review should contain one or two words, and no repeated words. Prove that no linear classifier using word features can get zero error on your dataset.Remember that this is a question about classifiers, not optimization algorithms; your proof should be true for any linear classifier, regardless of how the weights are learned.After providing such a dataset, propose a single additional feature that we could augment the feature vector with that would fix this problem. (Hint: think about the linear effect that each feature has on the classification score.)</li>

</ol>

Suppose that we are now interested in predicting a numeric rating for movie reviews. We will use a non-linear predictor that takes a movie review <span id="MathJax-Element-16-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-161" class="math"><span id="MathJax-Span-162" class="mrow"><span id="MathJax-Span-163" class="mi">x</span></span></span></span> and returns <span id="MathJax-Element-17-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-164" class="math"><span id="MathJax-Span-165" class="mrow"><span id="MathJax-Span-166" class="mi">σ</span><span id="MathJax-Span-167" class="mo">(</span><span id="MathJax-Span-168" class="texatom"><span id="MathJax-Span-169" class="mrow"><span id="MathJax-Span-170" class="mi">w</span></span></span><span id="MathJax-Span-171" class="mo">⋅</span><span id="MathJax-Span-172" class="mi">ϕ</span><span id="MathJax-Span-173" class="mo">(</span><span id="MathJax-Span-174" class="mi">x</span><span id="MathJax-Span-175" class="mo">)</span><span id="MathJax-Span-176" class="mo">)</span></span></span></span>, where <span id="MathJax-Element-18-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-177" class="math"><span id="MathJax-Span-178" class="mrow"><span id="MathJax-Span-179" class="mi">σ</span><span id="MathJax-Span-180" class="mo">(</span><span id="MathJax-Span-181" class="mi">z</span><span id="MathJax-Span-182" class="mo">)</span><span id="MathJax-Span-183" class="mo">=</span><span id="MathJax-Span-184" class="mo">(</span><span id="MathJax-Span-185" class="mn">1</span><span id="MathJax-Span-186" class="mo">+</span><span id="MathJax-Span-187" class="msubsup"><span id="MathJax-Span-188" class="mi">e</span><span id="MathJax-Span-189" class="texatom"><span id="MathJax-Span-190" class="mrow"><span id="MathJax-Span-191" class="mo">−</span><span id="MathJax-Span-192" class="mi">z</span></span></span></span><span id="MathJax-Span-193" class="msubsup"><span id="MathJax-Span-194" class="mo">)</span><span id="MathJax-Span-195" class="texatom"><span id="MathJax-Span-196" class="mrow"><span id="MathJax-Span-197" class="mo">−</span><span id="MathJax-Span-198" class="mn">1</span></span></span></span></span></span></span> is the logistic function that squashes a real number to the range <span id="MathJax-Element-19-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-199" class="math"><span id="MathJax-Span-200" class="mrow"><span id="MathJax-Span-201" class="mo">[</span><span id="MathJax-Span-202" class="mn">0</span><span id="MathJax-Span-203" class="mo">,</span><span id="MathJax-Span-204" class="mn">1</span><span id="MathJax-Span-205" class="mo">]</span></span></span></span>. Suppose that we wish to use the squared loss. For this problem, assume that the movie rating <span id="MathJax-Element-20-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-206" class="math"><span id="MathJax-Span-207" class="mrow"><span id="MathJax-Span-208" class="mi">y</span></span></span></span> is a real-valued variable in the range <span id="MathJax-Element-21-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-209" class="math"><span id="MathJax-Span-210" class="mrow"><span id="MathJax-Span-211" class="mo">(</span><span id="MathJax-Span-212" class="mn">0</span><span id="MathJax-Span-213" class="mo">,</span><span id="MathJax-Span-214" class="mn">1</span><span id="MathJax-Span-215" class="mo">)</span></span></span></span>.

<ol class="problem">

 <li id="2a" class="writeup">[2 points] Write out the expression for <span id="MathJax-Element-22-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-216" class="math"><span id="MathJax-Span-217" class="mrow"><span id="MathJax-Span-218" class="mtext">Loss</span><span id="MathJax-Span-219" class="mo">(</span><span id="MathJax-Span-220" class="mi">x</span><span id="MathJax-Span-221" class="mo">,</span><span id="MathJax-Span-222" class="mi">y</span><span id="MathJax-Span-223" class="mo">,</span><span id="MathJax-Span-224" class="texatom"><span id="MathJax-Span-225" class="mrow"><span id="MathJax-Span-226" class="mi">w</span></span></span><span id="MathJax-Span-227" class="mo">)</span></span></span></span>.</li>

 <li id="2b" class="writeup">[3 points] Compute the gradient of the loss.Hint: you can write the answer in terms of the predicted value <span id="MathJax-Element-23-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-228" class="math"><span id="MathJax-Span-229" class="mrow"><span id="MathJax-Span-230" class="mi">p</span><span id="MathJax-Span-231" class="mo">=</span><span id="MathJax-Span-232" class="mi">σ</span><span id="MathJax-Span-233" class="mo">(</span><span id="MathJax-Span-234" class="texatom"><span id="MathJax-Span-235" class="mrow"><span id="MathJax-Span-236" class="mi">w</span></span></span><span id="MathJax-Span-237" class="mo">⋅</span><span id="MathJax-Span-238" class="mi">ϕ</span><span id="MathJax-Span-239" class="mo">(</span><span id="MathJax-Span-240" class="mi">x</span><span id="MathJax-Span-241" class="mo">)</span><span id="MathJax-Span-242" class="mo">)</span></span></span></span>.</li>

 <li id="2c" class="writeup">[3 points] Assuming <span id="MathJax-Element-24-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-243" class="math"><span id="MathJax-Span-244" class="mrow"><span id="MathJax-Span-245" class="mi">y</span><span id="MathJax-Span-246" class="mo">=</span><span id="MathJax-Span-247" class="mn">1</span></span></span></span>, what is the smallest magnitude that the gradient can take? That is, find a way to set <span id="MathJax-Element-25-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-248" class="math"><span id="MathJax-Span-249" class="mrow"><span id="MathJax-Span-250" class="texatom"><span id="MathJax-Span-251" class="mrow"><span id="MathJax-Span-252" class="mi">w</span></span></span></span></span></span> to make <span id="MathJax-Element-26-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-253" class="math"><span id="MathJax-Span-254" class="mrow"><span id="MathJax-Span-255" class="mo">∥</span><span id="MathJax-Span-256" class="mi">∇</span><span id="MathJax-Span-257" class="mtext">Loss</span><span id="MathJax-Span-258" class="mo">(</span><span id="MathJax-Span-259" class="mi">x</span><span id="MathJax-Span-260" class="mo">,</span><span id="MathJax-Span-261" class="mi">y</span><span id="MathJax-Span-262" class="mo">,</span><span id="MathJax-Span-263" class="texatom"><span id="MathJax-Span-264" class="mrow"><span id="MathJax-Span-265" class="mi">w</span></span></span><span id="MathJax-Span-266" class="mo">)</span><span id="MathJax-Span-267" class="mo">∥</span></span></span></span> as small as possible. You are allowed to let the magnitude of <span id="MathJax-Element-27-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-268" class="math"><span id="MathJax-Span-269" class="mrow"><span id="MathJax-Span-270" class="texatom"><span id="MathJax-Span-271" class="mrow"><span id="MathJax-Span-272" class="mi">w</span></span></span></span></span></span> go to infinity. <i>Hint: try to understand intuitively what is going on and the contribution of each part of the expression. If you find doing too much algebra, you’re probably doing something suboptimal.</i>Motivation: the reason why we’re interested in the magnitude of the gradients is because it governs how far gradient descent will step. For example, if the gradient is close to zero when <span id="MathJax-Element-28-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-273" class="math"><span id="MathJax-Span-274" class="mrow"><span id="MathJax-Span-275" class="texatom"><span id="MathJax-Span-276" class="mrow"><span id="MathJax-Span-277" class="mi">w</span></span></span></span></span></span> is very far from the origin, then it could take a long time for gradient descent to reach the optimum (if at all). This is known as the <i>vanishing gradient problem</i> when training neural networks.</li>

 <li id="2d" class="writeup">[3 points] Assuming <span id="MathJax-Element-29-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-278" class="math"><span id="MathJax-Span-279" class="mrow"><span id="MathJax-Span-280" class="mi">y</span><span id="MathJax-Span-281" class="mo">=</span><span id="MathJax-Span-282" class="mn">1</span></span></span></span>, what is the largest magnitude that the gradient can take? Leave your answer in terms of <span id="MathJax-Element-30-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-283" class="math"><span id="MathJax-Span-284" class="mrow"><span id="MathJax-Span-285" class="mo">∥</span><span id="MathJax-Span-286" class="mi">ϕ</span><span id="MathJax-Span-287" class="mo">(</span><span id="MathJax-Span-288" class="mi">x</span><span id="MathJax-Span-289" class="mo">)</span><span id="MathJax-Span-290" class="mo">∥</span></span></span></span>.</li>

 <li id="2e" class="writeup">[3 points] The problem with the loss function we have defined so far is that is it is non-convex, which means that gradient descent is not guaranteed to find the global minimum, and in general these types of problems can be difficult to solve. So let us try to reformulate the problem as plain old linear regression. Suppose you have a dataset <span id="MathJax-Element-31-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-291" class="math"><span id="MathJax-Span-292" class="mrow"><span id="MathJax-Span-293" class="texatom"><span id="MathJax-Span-294" class="mrow"><span id="MathJax-Span-295" class="mi">D</span></span></span></span></span></span> consisting of <span id="MathJax-Element-32-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-296" class="math"><span id="MathJax-Span-297" class="mrow"><span id="MathJax-Span-298" class="mo">(</span><span id="MathJax-Span-299" class="mi">x</span><span id="MathJax-Span-300" class="mo">,</span><span id="MathJax-Span-301" class="mi">y</span><span id="MathJax-Span-302" class="mo">)</span></span></span></span> pairs, and that there exists a weight vector <span id="MathJax-Element-33-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-303" class="math"><span id="MathJax-Span-304" class="mrow"><span id="MathJax-Span-305" class="texatom"><span id="MathJax-Span-306" class="mrow"><span id="MathJax-Span-307" class="mi">w</span></span></span></span></span></span> that yields zero loss on this dataset. Show that there is an easy transformation to a modified dataset <span id="MathJax-Element-34-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-308" class="math"><span id="MathJax-Span-309" class="mrow"><span id="MathJax-Span-310" class="msup"><span id="MathJax-Span-311" class="texatom"><span id="MathJax-Span-312" class="mrow"><span id="MathJax-Span-313" class="mi">D</span></span></span><span id="MathJax-Span-314" class="mo">′</span></span></span></span></span> of <span id="MathJax-Element-35-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-315" class="math"><span id="MathJax-Span-316" class="mrow"><span id="MathJax-Span-317" class="mo">(</span><span id="MathJax-Span-318" class="mi">x</span><span id="MathJax-Span-319" class="mo">,</span><span id="MathJax-Span-320" class="msup"><span id="MathJax-Span-321" class="mi">y</span><span id="MathJax-Span-322" class="mo">′</span></span><span id="MathJax-Span-323" class="mo">)</span></span></span></span> pairs such that performing least squares regression (using a linear predictor and the squared loss) on <span id="MathJax-Element-36-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-324" class="math"><span id="MathJax-Span-325" class="mrow"><span id="MathJax-Span-326" class="msup"><span id="MathJax-Span-327" class="texatom"><span id="MathJax-Span-328" class="mrow"><span id="MathJax-Span-329" class="mi">D</span></span></span><span id="MathJax-Span-330" class="mo">′</span></span></span></span></span> converges to a vector <span id="MathJax-Element-37-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-331" class="math"><span id="MathJax-Span-332" class="mrow"><span id="MathJax-Span-333" class="msubsup"><span id="MathJax-Span-334" class="texatom"><span id="MathJax-Span-335" class="mrow"><span id="MathJax-Span-336" class="mi">w</span></span></span><span id="MathJax-Span-337" class="mo">∗</span></span></span></span></span> that yields zero loss on <span id="MathJax-Element-38-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-338" class="math"><span id="MathJax-Span-339" class="mrow"><span id="MathJax-Span-340" class="msup"><span id="MathJax-Span-341" class="texatom"><span id="MathJax-Span-342" class="mrow"><span id="MathJax-Span-343" class="mi">D</span></span></span><span id="MathJax-Span-344" class="mo">′</span></span></span></span></span>. Concretely, write an expression for <span id="MathJax-Element-39-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-345" class="math"><span id="MathJax-Span-346" class="mrow"><span id="MathJax-Span-347" class="msup"><span id="MathJax-Span-348" class="mi">y</span><span id="MathJax-Span-349" class="mo">′</span></span></span></span></span> in terms of <span id="MathJax-Element-40-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-350" class="math"><span id="MathJax-Span-351" class="mrow"><span id="MathJax-Span-352" class="mi">y</span></span></span></span> and justify this choice. This expression should not be a function of <span id="MathJax-Element-41-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-353" class="math"><span id="MathJax-Span-354" class="mrow"><span id="MathJax-Span-355" class="texatom"><span id="MathJax-Span-356" class="mrow"><span id="MathJax-Span-357" class="mi">w</span></span></span></span></span></span>.</li>

</ol>

<img decoding="async" data-src="sentiment.jpg" class="lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

 <noscript>

  <img decoding="async" src="sentiment.jpg">

 </noscript>

In this problem, we will build a binary linear classifier that reads movie reviews and guesses whether they are “positive” or “negative.” In this problem, you must implement the functions without using libraries like Scikit-learn.

<ol class="problem">

 <li id="3a" class="code">[2 points] Implement the function <code>extractWordFeatures</code>, which takes a review (string) as input and returns a feature vector <span id="MathJax-Element-42-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-358" class="math"><span id="MathJax-Span-359" class="mrow"><span id="MathJax-Span-360" class="mi">ϕ</span><span id="MathJax-Span-361" class="mo">(</span><span id="MathJax-Span-362" class="mi">x</span><span id="MathJax-Span-363" class="mo">)</span></span></span></span> (you should represent the vector <span id="MathJax-Element-43-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-364" class="math"><span id="MathJax-Span-365" class="mrow"><span id="MathJax-Span-366" class="mi">ϕ</span><span id="MathJax-Span-367" class="mo">(</span><span id="MathJax-Span-368" class="mi">x</span><span id="MathJax-Span-369" class="mo">)</span></span></span></span> as a <code>dict</code> in Python).</li>

 <li id="3b" class="code">[4 points] Implement the function <code>learnPredictor</code> using stochastic gradient descent and minimize the hinge loss. Print the training error and test error after each iteration to make sure your code is working. You must get less than 4% error rate on the training set and less than 30% error rate on the dev set to get full credit.</li>

 <li id="3c" class="code">[2 points] Create an artificial dataset for your <code>learnPredictor</code> function by writing the <code>generateExample</code> function (nested in the <code>generateDataset</code> function). Use this to double check that your <code>learnPredictor</code> works!</li>

 <li id="3d" class="writeup">[2 points] When you run the grader.py on test case <code>3b-2</code>, it should output a <code>weights</code> file and a <code>error-analysis</code> file. Look through some example incorrect predictions and for five of them, give a one-sentence explanation of why the classification was incorrect. What information would the classifier need to get these correct? In some sense, there’s not one correct answer, so don’t overthink this problem. The main point is to convey intuition about the problem.</li>

 <li id="3e" class="code">[2 points] Now we will try a crazier feature extractor. Some languages are written without spaces between words. So is splitting the words really necessary or can we just naively consider strings of characters that stretch across words? Implement the function <code>extractCharacterFeatures</code> (by filling in the <code>extract</code> function), which maps each string of <span id="MathJax-Element-44-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-370" class="math"><span id="MathJax-Span-371" class="mrow"><span id="MathJax-Span-372" class="mi">n</span></span></span></span> characters to the number of times it occurs, ignoring whitespace (spaces and tabs).</li>

 <li id="3f" class="writeup">[3 points] Run your linear predictor with feature extractor <code>extractCharacterFeatures</code>. Experiment with different values of <span id="MathJax-Element-45-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-373" class="math"><span id="MathJax-Span-374" class="mrow"><span id="MathJax-Span-375" class="mi">n</span></span></span></span> to see which one produces the smallest test error. You should observe that this error is nearly as small as that produced by word features. How do you explain this?Construct a review (one sentence max) in which character <span id="MathJax-Element-46-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-376" class="math"><span id="MathJax-Span-377" class="mrow"><span id="MathJax-Span-378" class="mi">n</span></span></span></span>-grams probably outperform word features, and briefly explain why this is so.</li>

</ol>

Suppose we have a feature extractor <span id="MathJax-Element-47-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-379" class="math"><span id="MathJax-Span-380" class="mrow"><span id="MathJax-Span-381" class="mi">ϕ</span></span></span></span> that produces 2-dimensional feature vectors, and a toy dataset <span id="MathJax-Element-48-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-382" class="math"><span id="MathJax-Span-383" class="mrow"><span id="MathJax-Span-384" class="msubsup"><span id="MathJax-Span-385" class="texatom"><span id="MathJax-Span-386" class="mrow"><span id="MathJax-Span-387" class="mi">D</span></span></span><span id="MathJax-Span-388" class="mtext">train</span></span><span id="MathJax-Span-389" class="mo">=</span><span id="MathJax-Span-390" class="mo">{</span><span id="MathJax-Span-391" class="msubsup"><span id="MathJax-Span-392" class="mi">x</span><span id="MathJax-Span-393" class="mn">1</span></span><span id="MathJax-Span-394" class="mo">,</span><span id="MathJax-Span-395" class="msubsup"><span id="MathJax-Span-396" class="mi">x</span><span id="MathJax-Span-397" class="mn">2</span></span><span id="MathJax-Span-398" class="mo">,</span><span id="MathJax-Span-399" class="msubsup"><span id="MathJax-Span-400" class="mi">x</span><span id="MathJax-Span-401" class="mn">3</span></span><span id="MathJax-Span-402" class="mo">,</span><span id="MathJax-Span-403" class="msubsup"><span id="MathJax-Span-404" class="mi">x</span><span id="MathJax-Span-405" class="mn">4</span></span><span id="MathJax-Span-406" class="mo">}</span></span></span></span> with

<ol type="1">

 <li><span id="MathJax-Element-49-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-407" class="math"><span id="MathJax-Span-408" class="mrow"><span id="MathJax-Span-409" class="mi">ϕ</span><span id="MathJax-Span-410" class="mo">(</span><span id="MathJax-Span-411" class="msubsup"><span id="MathJax-Span-412" class="mi">x</span><span id="MathJax-Span-413" class="mn">1</span></span><span id="MathJax-Span-414" class="mo">)</span><span id="MathJax-Span-415" class="mo">=</span><span id="MathJax-Span-416" class="mo">[</span><span id="MathJax-Span-417" class="mn">0</span><span id="MathJax-Span-418" class="mo">,</span><span id="MathJax-Span-419" class="mn">0</span><span id="MathJax-Span-420" class="mo">]</span></span></span></span></li>

 <li><span id="MathJax-Element-50-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-421" class="math"><span id="MathJax-Span-422" class="mrow"><span id="MathJax-Span-423" class="mi">ϕ</span><span id="MathJax-Span-424" class="mo">(</span><span id="MathJax-Span-425" class="msubsup"><span id="MathJax-Span-426" class="mi">x</span><span id="MathJax-Span-427" class="mn">2</span></span><span id="MathJax-Span-428" class="mo">)</span><span id="MathJax-Span-429" class="mo">=</span><span id="MathJax-Span-430" class="mo">[</span><span id="MathJax-Span-431" class="mn">0</span><span id="MathJax-Span-432" class="mo">,</span><span id="MathJax-Span-433" class="mn">2</span><span id="MathJax-Span-434" class="mo">]</span></span></span></span></li>

 <li><span id="MathJax-Element-51-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-435" class="math"><span id="MathJax-Span-436" class="mrow"><span id="MathJax-Span-437" class="mi">ϕ</span><span id="MathJax-Span-438" class="mo">(</span><span id="MathJax-Span-439" class="msubsup"><span id="MathJax-Span-440" class="mi">x</span><span id="MathJax-Span-441" class="mn">3</span></span><span id="MathJax-Span-442" class="mo">)</span><span id="MathJax-Span-443" class="mo">=</span><span id="MathJax-Span-444" class="mo">[</span><span id="MathJax-Span-445" class="mn">2</span><span id="MathJax-Span-446" class="mo">,</span><span id="MathJax-Span-447" class="mn">0</span><span id="MathJax-Span-448" class="mo">]</span></span></span></span></li>

 <li><span id="MathJax-Element-52-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-449" class="math"><span id="MathJax-Span-450" class="mrow"><span id="MathJax-Span-451" class="mi">ϕ</span><span id="MathJax-Span-452" class="mo">(</span><span id="MathJax-Span-453" class="msubsup"><span id="MathJax-Span-454" class="mi">x</span><span id="MathJax-Span-455" class="mn">4</span></span><span id="MathJax-Span-456" class="mo">)</span><span id="MathJax-Span-457" class="mo">=</span><span id="MathJax-Span-458" class="mo">[</span><span id="MathJax-Span-459" class="mn">1</span><span id="MathJax-Span-460" class="mo">,</span><span id="MathJax-Span-461" class="mn">2</span><span id="MathJax-Span-462" class="mo">]</span></span></span></span></li>

</ol>

<ol class="problem">

 <li id="4a" class="writeup">[2 points] Run 2-means on this dataset until convergence. Please show your work. What are the final cluster assignments <span id="MathJax-Element-53-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-463" class="math"><span id="MathJax-Span-464" class="mrow"><span id="MathJax-Span-465" class="mi">z</span></span></span></span> and cluster centers <span id="MathJax-Element-54-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-466" class="math"><span id="MathJax-Span-467" class="mrow"><span id="MathJax-Span-468" class="mi">μ</span></span></span></span>? Run this algorithm twice with the following initial centers:

  <ol type="1">

   <li><span id="MathJax-Element-55-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-469" class="math"><span id="MathJax-Span-470" class="mrow"><span id="MathJax-Span-471" class="msubsup"><span id="MathJax-Span-472" class="mi">μ</span><span id="MathJax-Span-473" class="mn">1</span></span><span id="MathJax-Span-474" class="mo">=</span><span id="MathJax-Span-475" class="mo">[</span><span id="MathJax-Span-476" class="mn">1</span><span id="MathJax-Span-477" class="mo">,</span><span id="MathJax-Span-478" class="mn">3</span><span id="MathJax-Span-479" class="mo">]</span></span></span></span> and <span id="MathJax-Element-56-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-480" class="math"><span id="MathJax-Span-481" class="mrow"><span id="MathJax-Span-482" class="msubsup"><span id="MathJax-Span-483" class="mi">μ</span><span id="MathJax-Span-484" class="mn">2</span></span><span id="MathJax-Span-485" class="mo">=</span><span id="MathJax-Span-486" class="mo">[</span><span id="MathJax-Span-487" class="mn">1</span><span id="MathJax-Span-488" class="mo">,</span><span id="MathJax-Span-489" class="mo">−</span><span id="MathJax-Span-490" class="mn">1</span><span id="MathJax-Span-491" class="mo">]</span></span></span></span></li>

   <li><span id="MathJax-Element-57-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-492" class="math"><span id="MathJax-Span-493" class="mrow"><span id="MathJax-Span-494" class="msubsup"><span id="MathJax-Span-495" class="mi">μ</span><span id="MathJax-Span-496" class="mn">1</span></span><span id="MathJax-Span-497" class="mo">=</span><span id="MathJax-Span-498" class="mo">[</span><span id="MathJax-Span-499" class="mo">−</span><span id="MathJax-Span-500" class="mn">1</span><span id="MathJax-Span-501" class="mo">,</span><span id="MathJax-Span-502" class="mn">1</span><span id="MathJax-Span-503" class="mo">]</span></span></span></span> and <span id="MathJax-Element-58-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-504" class="math"><span id="MathJax-Span-505" class="mrow"><span id="MathJax-Span-506" class="msubsup"><span id="MathJax-Span-507" class="mi">μ</span><span id="MathJax-Span-508" class="mn">2</span></span><span id="MathJax-Span-509" class="mo">=</span><span id="MathJax-Span-510" class="mo">[</span><span id="MathJax-Span-511" class="mn">2</span><span id="MathJax-Span-512" class="mo">,</span><span id="MathJax-Span-513" class="mn">2</span><span id="MathJax-Span-514" class="mo">]</span></span></span></span></li>

  </ol></li>

 <li id="4b" class="code">[5 points] Implement the <code>kmeans</code> function. You should initialize your <span id="MathJax-Element-59-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-515" class="math"><span id="MathJax-Span-516" class="mrow"><span id="MathJax-Span-517" class="mi">k</span></span></span></span> cluster centers to random elements of <code>examples</code>. After a few iterations of k-means, your centers will be very dense vectors. In order for your code to run efficiently and to obtain full credit, you will need to precompute certain quantities. As a reference, our code runs in under a second on Myth, on all test cases. You might find <code>generateClusteringExamples</code> in util.py useful for testing your code. In this problem, you are not allowed to use libraries like Scikit-learn.</li>

 <li id="4c" class="writeup">[5 points] Sometimes, we have prior knowledge about which points should belong in the same cluster. Suppose we are given a set <span id="MathJax-Element-60-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-518" class="math"><span id="MathJax-Span-519" class="mrow"><span id="MathJax-Span-520" class="mi">S</span></span></span></span> of example pairs <span id="MathJax-Element-61-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-521" class="math"><span id="MathJax-Span-522" class="mrow"><span id="MathJax-Span-523" class="mo">(</span><span id="MathJax-Span-524" class="mi">i</span><span id="MathJax-Span-525" class="mo">,</span><span id="MathJax-Span-526" class="mi">j</span><span id="MathJax-Span-527" class="mo">)</span></span></span></span> which must be assigned to the same cluster. For example, suppose we have 5 examples; then <span id="MathJax-Element-62-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-528" class="math"><span id="MathJax-Span-529" class="mrow"><span id="MathJax-Span-530" class="mi">S</span><span id="MathJax-Span-531" class="mo">=</span><span id="MathJax-Span-532" class="mo">{</span><span id="MathJax-Span-533" class="mo">(</span><span id="MathJax-Span-534" class="mn">1</span><span id="MathJax-Span-535" class="mo">,</span><span id="MathJax-Span-536" class="mn">5</span><span id="MathJax-Span-537" class="mo">)</span><span id="MathJax-Span-538" class="mo">,</span><span id="MathJax-Span-539" class="mo">(</span><span id="MathJax-Span-540" class="mn">2</span><span id="MathJax-Span-541" class="mo">,</span><span id="MathJax-Span-542" class="mn">3</span><span id="MathJax-Span-543" class="mo">)</span><span id="MathJax-Span-544" class="mo">,</span><span id="MathJax-Span-545" class="mo">(</span><span id="MathJax-Span-546" class="mn">3</span><span id="MathJax-Span-547" class="mo">,</span><span id="MathJax-Span-548" class="mn">4</span><span id="MathJax-Span-549" class="mo">)</span><span id="MathJax-Span-550" class="mo">}</span></span></span></span> says that examples 2, 3, and 4 must be in the same cluster and that examples 1 and 5 must be in the same cluster. Provide the modified k-means algorithm that performs alternating minimization on the reconstruction loss.<i>Recall that alternating minimization is when we are optimizing two variables jointly by alternating which variable we keep constant.</i></li>

</ol>

5/5 - (2 votes)

This (and every) assignment has a written part and a programming part.

The full assignment with our supporting code and scripts can be downloaded as <a href="../sentiment.zip">sentiment.zip</a>.

<ol class="problem">

 <li class="writeup template">This icon means a written answer is expected in <code>sentiment.pdf</code>.</li>

 <li class="code template">This icon means you should write code in <code><a href="submission.py">submission.py</a></code>.</li>

</ol>

You should modify the code in <code><a href="submission.py">submission.py</a></code> between

<pre># BEGIN_YOUR_CODE</pre>

and

<pre># END_YOUR_CODE</pre>

but you can add other helper functions outside this block if you want. Do not make changes to files other than <code><a href="submission.py">submission.py</a></code>.Your code will be evaluated on two types of test cases, <b>basic</b> and <b>hidden</b>, which you can see in <code><a href="grader.py">grader.py</a></code>. Basic tests, which are fully provided to you, do not stress your code with large inputs or tricky corner cases. Hidden tests are more complex and do stress your code. The inputs of hidden tests are provided in <code><a href="grader.py">grader.py</a></code>, but the correct outputs are not. To run the tests, you will need to have <code><a href="graderUtil.py">graderUtil.py</a></code> in the same directory as your code and <code><a href="grader.py">grader.py</a></code>. Then, you can run all the tests by typing

<pre>python grader.py</pre>

This will tell you only whether you passed the basic tests. On the hidden tests, the script will alert you if your code takes too long or crashes, but does not say whether you got the correct output. You can also run a single test (e.g., <code>3a-0-basic</code>) by typing

<pre>python grader.py 3a-0-basic</pre>

We strongly encourage you to read and understand the test cases, create your own test cases, and not just blindly run <code><a href="grader.py">grader.py</a></code>.

<hr>

<b></b>General Instructions

Problem 1: Warmup

<span id="MathJax-Element-10-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-50" class="math"><span id="MathJax-Span-51" class="mrow"><span id="MathJax-Span-52" class="msubsup"><span id="MathJax-Span-53" class="mtext">Loss</span><span id="MathJax-Span-54" class="texatom"><span id="MathJax-Span-55" class="mrow"><span id="MathJax-Span-56" class="mtext">hinge</span></span></span></span><span id="MathJax-Span-57" class="mo">(</span><span id="MathJax-Span-58" class="mi">x</span><span id="MathJax-Span-59" class="mo">,</span><span id="MathJax-Span-60" class="mi">y</span><span id="MathJax-Span-61" class="mo">,</span><span id="MathJax-Span-62" class="texatom"><span id="MathJax-Span-63" class="mrow"><span id="MathJax-Span-64" class="mi">w</span></span></span><span id="MathJax-Span-65" class="mo">)</span><span id="MathJax-Span-66" class="mo">=</span><span id="MathJax-Span-67" class="mo">max</span><span id="MathJax-Span-68" class="mo">{</span><span id="MathJax-Span-69" class="mn">0</span><span id="MathJax-Span-70" class="mo">,</span><span id="MathJax-Span-71" class="mn">1</span><span id="MathJax-Span-72" class="mo">−</span><span id="MathJax-Span-73" class="texatom"><span id="MathJax-Span-74" class="mrow"><span id="MathJax-Span-75" class="mi">w</span></span></span><span id="MathJax-Span-76" class="mo">⋅</span><span id="MathJax-Span-77" class="mi">ϕ</span><span id="MathJax-Span-78" class="mo">(</span><span id="MathJax-Span-79" class="mi">x</span><span id="MathJax-Span-80" class="mo">)</span><span id="MathJax-Span-81" class="mi">y</span><span id="MathJax-Span-82" class="mo">}</span><span id="MathJax-Span-83" class="mo">,</span></span></span></span>

<span id="MathJax-Element-12-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-87" class="math"><span id="MathJax-Span-88" class="mrow"><span id="MathJax-Span-89" class="texatom"><span id="MathJax-Span-90" class="mrow"><span id="MathJax-Span-91" class="mi">w</span></span></span><span id="MathJax-Span-92" class="mo">←</span><span id="MathJax-Span-93" class="texatom"><span id="MathJax-Span-94" class="mrow"><span id="MathJax-Span-95" class="mi">w</span></span></span><span id="MathJax-Span-96" class="mo">−</span><span id="MathJax-Span-97" class="mi">η</span><span id="MathJax-Span-98" class="msubsup"><span id="MathJax-Span-99" class="mi">∇</span><span id="MathJax-Span-100" class="texatom"><span id="MathJax-Span-101" class="mrow"><span id="MathJax-Span-102" class="mi">w</span></span></span></span><span id="MathJax-Span-103" class="msubsup"><span id="MathJax-Span-104" class="mtext">Loss</span><span id="MathJax-Span-105" class="texatom"><span id="MathJax-Span-106" class="mrow"><span id="MathJax-Span-107" class="mtext">hinge</span></span></span></span><span id="MathJax-Span-108" class="mo">(</span><span id="MathJax-Span-109" class="mi">x</span><span id="MathJax-Span-110" class="mo">,</span><span id="MathJax-Span-111" class="mi">y</span><span id="MathJax-Span-112" class="mo">,</span><span id="MathJax-Span-113" class="texatom"><span id="MathJax-Span-114" class="mrow"><span id="MathJax-Span-115" class="mi">w</span></span></span><span id="MathJax-Span-116" class="mo">)</span><span id="MathJax-Span-117" class="mo">,</span></span></span></span>

Problem 2: Predicting Movie Ratings

Problem 3: Sentiment Classification