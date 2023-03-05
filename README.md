# two-days
if( $ShowAllUserDetails){
                     $connection = $this->resource->getConnection();
                     $posUserId= $this->supermaxSession->getPosUserId();
                     $userDataCollection = $this->supermaxUserCollection
                     ->addFieldToFilter('pos_user_id', $posUserId );
                     $userData = $userDataCollection->getData();
-                    if(!empty($userData)) {
-                    $posOutletId = $userData[0]['pos_outlet_id'];
-                    $connection = $this->resource->getConnection();  
-                    $supermaxHoldCartTable = $connection->getTableName('ah_supermax_pos_hold_carts');
-                    $to = date("Y-m-d"); 
-                    $from = strtotime('-'.$HoldCartDayInterval.' day', strtotime($to));
-                    $from = date('Y-m-d', $from);    
-                    $select = $connection->select()
-                            ->from(
-                        ['p' => $supermaxHoldCartTable])
-                          ->where("DATE(create_date) >= '$from' And DATE(create_date) <= '$to' ");
-                        $result = $connection->fetchAll($select);
-
-                   }
+                }
+                 } else {
+                 $error = true;
+                    }
+        } catch (\Exception $e) {
+         dump($e);
+         $error = true;
+        }
+        $data = array('error' => $error, 'result' => $result);
+         return json_encode($data);
         }
-    } catch (\Exception $e) {
-        dump($e);
-        $error = true;
-}
-$data = array('error' => $error, 'result' => $result);
-return json_encode($data);
-}
-
