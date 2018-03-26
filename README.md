# Group-13-ortec-solution
Colaboratory repository: https://drive.google.com/file/d/1XJJiMVrIuNLBPC7hem8ijVq52H7evH__/view?usp=sharing

Ortec Finance Invoice Solution (group 13)

This readme file contains all the documentation of our Ortec Finance Invoice solution, part of Bletchley: machine learning in a financial context bootcamp organized by Turing Society, B&R Beurs and IFSA at Erasmus University Rotterdam.

Goal of the application:

Create an application that identifies relevant information from text-format invoices and correctly outputs this to the right category. The categories are:

- Ignore (nonrelevant information)
- Sender name
- Sender Chamber of Commerce number
- Sender IBAN
- Invoice Reference
- Total

A baseline has been provided for the application by Jannes Klaas, head instructor of Bletchley: machine learning in a financial context bootcamp. Provided baseline has been used to create an improved solution.

Implementation

A limited amount of training data has been provided by the client (two invoice templates to be exact). We used the baseline invoice creator in the provded templates to create test and validation data. Afterwards we ran the baseline neural net thrice and average the outputs in order to lower the error rate (bagging).

Next we applied a convolution filter over the output, so that small islands (e.g. 500550000, gaps (555505555) and 'weak' edge states (in strings of e.g. 05*5550) (5* being a weak edge state) have their weights lowered. We scaled all found falues for 0 (the none-category) with 1.25(scaling with 1.25 is an experimentally found value), to account for the imbalanced ratio of symbols labeled with a 0, as compared to those labeled anything else//'false positives' were found to be most abundant: Train of thought: if the algorithm finds that it can be a zero, it probably is. 
The categories that involve specific strings (s.a. IBAN and max value owed) can be searched deterministially. If either of these two can be found, then we first reset the outputs of said categories, found by machinelearning, and then overwrite.

The present model's results:

No proper quantitative large-scaled analysis has been performed, though the filter, the scaling and the deterministic seem to
consistently clean up the outcome of the neural net. The target 1-5's are pretty much always labeled correctly, 
the target 0's occasionally become victims of false positives. The accuracy on a single invoice can be verified in the last few lines.

Contraints

-Due to the limited amount of training data provided there is a probability the model presented overfits and therefore will not generalize effectively.

-Accuracy will differ with each input model (and with different invoices too) but the variance between different models (after the bagging/averaging) should not be too high

What should still be done / Reflection
With a larger dataset we believe the model will generalize correctly. Next to this, better quantitative metrics should be implemented in order to evaluate the performance of the algorithm. 

For an updated version we want to make the application webbased with the use of the Django framework:
- Upload data thats needs to be evaluated to the back end
- Application evaluates and categorizes the data
- Data is pushed to Entity–relationship model and correctly accounted for
- Sample-wise testing of performance by human/auditor
