Title: Why You Need Pipelines with SKLearn
Date: 2021-10-12 20:30
Category: Data Science

SKLearn is an immensley popular tool for machine learning. One of its slightly more unwieldy tools is [pipelines](https://scikit-learn.org/stable/modules/generated/sklearn.pipeline.Pipeline.html).
It is also overlooked when first teaching people to use SKLearn in introductory courses to machine learning.
This is a real shame, because it can help prevent one of the most common errors that those who dabbel in data
science commit - data leakage.

Data leakage in this case, happens when we infer values from a data set.
However, when we split the data into test and train data sets, we sometimes forget that we're not supposed to be able
to peek in at the test data set _at all_.
This means that we cannot use that data to inform our thinking about how to approach the problem.
So a classic example of this occurs when we infer missing values from a data set.
If you infer missing values by, say replacing the missing values with the median value and _then_ splitting
the data set in to test and train, then we have already taken a peek and 'learned' from data that we are soon going to be asked to predict.
The result is that your model's performance will now be ever so over-stated.

However, we're often taught about the dangers of data leakage, warned against every doing it and not really given the tools to prevent shooting ourselves in the foot.
Because inevitably you're going to start using cross-validatiton, where you take your training data and split it in to further chunks of test and train data.
When this happens, any values that you inferred for say the mean or median value are leaking data.
This is what Pipelines can help us to avoid from the get-go!

By setting up the _process_ that needs to occur to the data, and then giving the training data to something like `GridSearch`, which uses cross-validation to determine what the best model or approach might be, then we avoid the problem altogether. The Pipeline ensures that the median value generated each time has not been influenced by the test data.

And _that_ children is why we always use a Pipeline.
