# Deferred CDO Coupon Payment Valuation Model
 

The deferred CDO coupon payment valuation model serves the purpose of valuing the accumulated coupon payments held in a non-interest-bearing reserve account for a CDO trade.  It is a part of the valuation model for a non-vanilla CDO structure called “rated equity.”

The model is a straightforward extension of the existing valuation model for vanilla CDO trades. The amount of each deferred coupon payment is calculated the same way as a vanilla CDO trade. Because the reserve account is non-interest-bearing, all the cash flows held in the account are discounted using the discount factor at the trade maturity. Note that for an interest-bearing reserve account, accumulated coupon payments are valued in the same as a vanilla CDO trade case and no new model is required.

The model serves the purpose of computing the value of the accumulated coupon payments held in the non-interest-bearing reserve account for a CDO trade [1]. It is a part of the valuation model for a non-vanilla CDO trade called “rated equity”, which is defined as an equity tranche with part of its coupon payments held in a reserve account. 

Modeling the accumulated coupon payments (see https://finpricing.com/lib/FiBondCoupon.html) is straightforward within the current structured credit derivative modeling framework. The amount of each coupon payment is calculated the same way as a vanilla CDO trade. Because the reserve account is non-interest-bearing, all the cash flows held in the account are discounted using an appropriate discount factor at the trade maturity. Note that for an interest bearing reserve account, accumulated coupon payments are valued in the same way as that for a vanilla CDO trade and no new model is required.

Assume that the collateral pool is tranched into several tranches with the tranche defined by an attachment point , a detachment point , and a fixed time horizon   with fee payments at intervals .   We first define the loss function of the collateral pool:

(1)		 ,		

where    is the loss given default (LGD) for the  reference name.   The expected loss function of the tranche has the form

(2)		 

The value of the accumulated coupon payments can be calculated readily:

Annuity of the fee leg: interesting-bearing:

 (3)		 ,


Annuity of the fee leg: non-interesting-bearing:

 (4)		 ,

with the first term being the annuity of the fee payment stream and the second the fee accrual.  )  is the thickness of the tranche. Payment for the fee during the period   is made at  ;   is the day count fraction; D(t) is the discount factor.
For a “rated equity” trade with retained coupon payment spread , the value of the reserve account is 

(5)		 .

Note that the submitted model is for the non-interest-bearing reserve account, which is described by Eq. (4). We can see from Eq. (3) that, for the interest-bearing account, the computation of the value is the same as the valuation of the fee leg for a vanilla CDO trade [2]. 

As shown in Eqs. (3) and (4), the valuation of the reserve account is dependent on the default correlation model, which is employed to calculate the expected loss of the tranche. In the submitted model, a semi-closed normal copula model and a base correlation model framework are employed, which is considered the current market standard modeling approach for the structured credit derivatives. 

The model is different from a vanilla CDO model in terms of the treatment of discounting. The model is straightforward and it not necessary to test against other benchmark models.

Two series of testing were designed to investigate the model. First, the submitted model was tested by an independent implementation of the model via existing approved models for vanilla CDO trades in the Oscar-Fritz library. By manipulating the discount factor, we replicated the value of the accumulated coupon payments without-interest-bearing using a vanilla CDO model. Assuming a zero discount factor, we calculated the accumulated coupon payments using the vanilla CDO model. The value of the reserve account was then computed by discounting these fee payments with discount factor at trade maturity. 

Second, we calculated the risk free accumulated coupon payments by setting a 100% recovery rate for each obligor of the test trade. This risk free reserve account value can be easily tested through a spreadsheet function.

The annuities of the coupon payments for the test trade under the various scenarios calculated by the model and an independent test model. It can be seen that they are identical, indicating that the submitted model is implemented correctly.

As a second series of testing, we set the recovery rate of each obligor of the test trade be 100%. In this scenario although there are default events in the collateral pool, the expected loss will be zero over time hence Eq.(3) simply becomes:

(6)	 ,

if we assume the day count convention for the fee leg be ACT/365. Once we export the discount factor , Eq. (6) can be easily verified by a spreadsheet function. 

The model for the valuation of the accumulated coupon payments held in the non-interest-bearing reserve account for a CDO trade has been investigated. Tests have shown that the submitted model serves the intended purpose and has been implemented correctly. 

The submitted mode is a part of the valuation model for a non-vanilla CDO trade called “rated equity,” which is defined as an equity tranche with part of its coupon payments held in a reserve account. The accumulated coupon payments are used to absorb the credit events and the leftover will be paid out to the investor at the trade maturity. 

Modeling the accumulated coupon payments is straightforward within the current structured credit derivative modeling framework. The amount of each coupon payment is calculated based on the outstanding notional amount and retained coupon level, following the same way as that for a vanilla CDO trade. Because the reserve account is non-interest-bearing, all the cash flows held in the account are discounted using the appropriate discount factor at the trade maturity. For an interest bearing reserve account, accumulated coupon payments are valued in the same way as a vanilla CDO trade and no new model is required.

Note that the submitted model only applies to the reserve account in which no interest is earned. At the present time, the model has to employ the semi-closed form normal copula default correlation model. 

