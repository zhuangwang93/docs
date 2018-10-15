This file shows the function invocations of SKB process in the kernel.
# Transmit a packet
Include kernel functions from __tcp_transmit_skb() in the TCP layer to ixgbe_xmit_frame_ring() in the ethernet.
The function invocation process from tcp_msgsend() to __tcp_transmit_skb() can be found in [RTT.md](https://github.com/alvenwong/docs/blob/master/RTT.md). <p>
__tcp_transmit_skb <br>
-> ip_queue_xmit <br>
-> ip_local_out <br>
-> __ip_local_out <br>
-> dst_output <br>
-> ip_output <br>
-> ip_finish_output <br>
-> ip_finish_output_gso <br>
-> ip_finish_output2 <br>
-> dst_neigh_output <br>
-> neigh_hh_output <br>
-> dev_queue_xmit <br>
-> __dev_queue_xmit <br>
-> __dev_xmit_skb <br>
-> sch_direct_xmit <br>
-> dev_hard_start_xmit <br>
-> xmit_one <br>
-> netdev_start_xmit <br>
-> __netdev_start_xmit <br>
-> ixgbe_xmit_frame <br>
-> __ixgbe_xmit_frame <br>
-> ixgbe_xmit_frame_ring <br>

# Receive a packet
Include kernel functions from ixgbe_poll() in the ethernet to skb_copy_datagram_iter() in the TCP layer.
ixgbe_poll() <br>
-> ixgbe_clean_rx_irq() <br>
-> |- ixgbe_process_skb_fields() (from this function, skb is one of the arguments) -> eth_type_trans() <br>
-> |- ixgbe_rx_skb() -> <br>
(napi_gro_receive()) <br>
-> netif_rx() <br>
-> netif_rx_action() <br>
-> netif_receive_skb_internal() <br>
->  __netif_receive_skb() <br>
->  __netif_receive_skb_core() <br>
-> deliver_skb() <br>
-> ip_rcv() <br>
-> ip_rcv_finish() <br>
-> ip_route_input_noref() <br>
-> tcp_v4_rcv() -> tcp_v4_fill_cb() <br>
-> tcp_v4_do_rcv() <br>
-> tcp_rcv_established() (sk->sk_state == TCP_ESTABLISHED) <br>
-> tcp_data_queue() <br>
-> tcp_queue_rcv() -> tcp_event_data_recv() <br>
-> __skb_queue_tail -> skb_set_owner_r() <br>

skb_copy_datagram_iter() <br>
sock_def_readable() <br>