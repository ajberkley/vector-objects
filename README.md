# vector-objects
I used this when I was doing server side drawing of wind arrows on canadarasp.com.  It turned
    out better to just do it in javascript client side (it wasn't as fast, but it cost less in AWS
    fees and I could do easier dynamic scaling, etc).
    For drawing on a PNG an arrow withx and y components u and v:
```lisp
   (with-drawable-image (draw image y-size x-size)
     (draw-lines (manipulate-object* *prototype-arrow*
                                     :rotate (- (float (atan v u) 0f0))
                                     :scale (* scale (/ (- scale 1f0) scale))
                                     :translate (point (float (* scale (- x x-pixel-min -0.5)) 0f0)
                                                       (float (* scale (- y y-pixel-min -0.5)) 0f0)))
               (lambda (x y)
                 (declare (type (integer -100000 10000000) x y))
                 (when (and (>= x 0) (>= y 0)
                            (< x x-size) (< y y-size))
                   (draw x y 255 0 255))))```
