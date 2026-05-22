## What is Jacobian 


In 2D dimenions we say linear map when it follows three points - 
1. Parallel lines stay parallel after transformation of linear map.  - After transformation line should be parallel.
2. Even spacing must even after transformation. 
3. But the map must be fixed throughout all of the transformation.

**Determinant** - 
In 2D map, it defines the scaling facotr of area between before and after transformation. 

**Derivates in 1D**
Derivates in 1D tells the local scaling facotr, means if you derivate the function and zoom in at the particular point then you find that by how much its neighbouring points get strecthed or shrinked. We dont all of the points with respect to that point because the function stretches and shrinkes that whole line in different different way. We have to go infinitely close to see this effect. <br>
Even for the same function, the Jacobian and the derivative can be different depending on *a* means Agar hum kisi function ko ek specific point par zoom in karke dekhte hain, toh wahan scaling factor (derivative) kuch aur ho sakta hai (jaise video ke example mein ek point par yeh factor 3 tha).  Lekin agar hum usi same function mein apna point 'a' kisi doosri jagah shift kar dein, toh function ka behavior wahan bilkul alag ho sakta hai. Ho sakta hai nayi jagah par function points ko palat raha ho (reflection) aur 2 guna stretch kar raha ho, jiske karan us naye point par derivative -2 ho jayega. <br>

**Derivates in 2D**
In 2D functions we have 2 inputs and 2 outputs. When we transform the function means than all of the straight lines got curved or distorted. Now after transformation, we have to focus on one point (a,b). When we focus or zoomr on that particular point then that distorted lines becomes straight and seems like linear map. Usually that small part is not straght line but it is seems like perfectly straight line. For further calculation we chose best or approximate straight line map. <br>
Usi "best match" waale linear map ki jaankaari dene k liye jo 4 numbers ka matrix bnta hai usko hum Jacobian matrix kehte hai. <br>
Now to get this matrix we need split the original function *f* into 2 parts - *f1* tells the x-cordinate of output. f2 tells the y-cordinate of output.  <br>
Now we need to see, how these matrix form - <br>
**first column** - <br>
Horizontal Movement ka asar - Pehla column yeh batata hai ki agar hum point (a,b) se sirf horizontal direction (right side) mein thoda sa aage badhein, toh kya hoga. <br>
Isko nikalne ke liye hum ek temporary 1D function g sochte hain. Function g mein hum y-input ko fix kar dete hain aur sirf x-axis ke along move karte hain. Function g ka derivative, g′(a), humein batata hai ki horizontal movement karne par naya x-coordinate kitna scale hua. Ye humare matrix ka pehle column ka upar wala number hota hai. <br>
Usi tarah, ek aur function h sochte hain jo isi horizontal movement ka asar y-coordinate par batata hai. h′ (a) humare pehle column ka neeche wala number ban jata hai. To basically ye x point ka horizontal shift btate hai.
**Second Column** <br>
Doosra column yeh batata hai ki agar hum point (a,b) se sirf vertical direction (upar) mein aage badhein, toh kya hoga. Iske liye hum x-input ko fix kar dete hain aur do naye function p aur q sochte hain jo vertical line par focus karte hain.  <br>
Function p ka derivative, p′(b), nikalta hai jo batata hai ki naya x-coordinate kahan gaya. unction q ka derivative, q'(b) , batata hai ki naya y-coordinate kahan gaya. Ye dono numbers doosre column mein aate hain.
*(Note: Maths mein in temporary functions ke derivatives nikalne ke is process ko Partial Derivatives kaha jata hai)* <br>
**Jab humara ye 4 numbers ka Jacobian matrix ban kar taiyaar ho jata hai, toh hum uska Determinant calculate kar sakte hain. Ye Jacobian determinant humein ek final number deta hai jo batata hai ki: Point (a,b) ke bilkul aas-paas ke chote se ilake ka Area kis factor se scale hua hai (badha ya ghata hai)** <br>
 Humara main goal sirf ye dekhna nahi hota ki point (a,b) kahan gaya, balki hum ye janna chahte hain ki us point ke bilkul aas-paas ka ilaka (neighbouring points) f function apply hone ke baad kis tarah transform hua ya bada/ghata. 



