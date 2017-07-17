# onedirective.js-to-secdirective.js-data-pass

onedirective.js (Which is send data to another directive in angular js)
$rootScope inject to app controller.

  scope.ChangeOrder = function (type, reverse) {
               // debugger;
                scope.sort = type;
                scope.sortReverse = reverse;
                console.log(scope.docketlist);
                $rootScope.$broadcast('orderDate', { type: type, reverse: reverse });
               
            }
secdirective.js 

      $rootScope.$on('orderDate', function (event, data) {
                scope.docketlist = scope.docketlist.sort(scope.GetSortOrder(data.type, data.reverse));
               
            });
            scope.GetSortOrder = function (prop, reverse) {
                return function (a, b) {
                    if (reverse) {
                        return new Date(b[prop]).getTime() - new Date(a[prop]).getTime()
                    } else {
                        return new Date(a[prop]).getTime() - new Date(b[prop]).getTime()
                    }
                }
            }
            
