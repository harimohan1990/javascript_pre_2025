# javascript_pre_2025

#array method polyfiils 

forEach
Array.prototype.ourForEach = function (callBack) {
  for (let i = 0; i < this.length; i++) {
    callBack(this[i]);
  }
};
names.ourForEach(consoleFunc);
