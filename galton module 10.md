#You may recall that, with this data set, obvious regressors for a child's adult height would be the height of the parents. 

#1) Run the regression using parents' heights alone as the only regressors.  Report parameter values, parameter p-values, and R2adj for the model.

parent.height.lm= lm(galton$adult.child.height~galton$father+galton$mother) 
summ=summary(parent.height.lm)
summ$adj.r.squared
summ$coefficients

qqnorm(parent.height.lm$residuals)
qqline(parent.height.lm$residuals)



#Of course, the gender of the child would also seem to play a very important role.  What is still uncertain is whether two way interactions play a role.

#2) Run a model using parents' individual heights, child gender, and all three possible two way interactions.  Do not simply multiply the three regressors together in R, as, while that will give us all of the terms we want, it will also give us a three-way interaction that we don't want between both parents' heights and child's gender (three-way interactions are very rare).  Report parameter values, parameter p-values, and R2adj for the model.

interactions.lm= lm(adult.child.height~father+mother+as.factor(gender)+father:mother+father:as.factor(gender)+mother:as.factor(gender), galton)
summ2=summary(interactions.lm)
summ2$adj.r.squared
summ2$coefficients

##3) Run a model with no interactions.  Report parameter values, parameter p-values, and R2adj for the model.

no.interactions.lm= (galton$adult.child.height~galton$father+galton$mother+as.factor(galton$gender)
summ3=summary(no.interactions.lm)
summ3$adj.r.squared
summ3$coefficients

4) For the last model, perform the residual analysis by finding the qq plot for normality, as well as R student residuals vs. predicted, color coded by child's gender.

plot(fitted(no.interactions.lm), rstudent(no.interactions.lm), 
col = as.factor(galton$gender))

5) Comment on which model you think is best.

