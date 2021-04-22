<template>
  <div class="wrapper">
    <div class="content">
      <button @click="btnClick">按钮</button>
      <li>fenglei1</li>
      <li>fenglei2</li>
      <li>fenglei3</li>
      <li>fenglei4</li>
      <li>fenglei5</li>
      <li>fenglei6</li>
      <li>fenglei7</li>
      <li>fenglei8</li>
      <li>fenglei9</li>
      <li>fenglei10</li>
      <li>fenglei11</li>
      <li>fenglei12</li>
      <li>fenglei13</li>
      <li>fenglei14</li>
      <li>fenglei15</li>
      <li>fenglei16</li>
      <li>fenglei17</li>
      <li>fenglei18</li>
      <li>fenglei19</li>
      <li>fenglei20</li>
      <li>fenglei21</li>
      <li>fenglei22</li>
      <li>fenglei23</li>
      <li>fenglei24</li>
      <li>fenglei25</li>
      <li>fenglei26</li>
      <li>fenglei27</li>
      <li>fenglei28</li>
      <li>fenglei29</li>
      <li>fenglei30</li>
      <li>fenglei31</li>
      <li>fenglei32</li>
      <li>fenglei33</li>
      <li>fenglei34</li>
      <li>fenglei35</li>
      <li>fenglei36</li>
      <li>fenglei37</li>
      <li>fenglei38</li>
      <li>fenglei39</li>
      <li>fenglei40</li>
      <li>fenglei41</li>
      <li>fenglei42</li>
      <li>fenglei43</li>
      <li>fenglei44</li>
      <li>fenglei45</li>
      <li>fenglei46</li>
      <li>fenglei47</li>
      <li>fenglei48</li>
      <li>fenglei49</li>
      <li>fenglei50</li>
      <li>fenglei51</li>
      <li>fenglei52</li>
      <li>fenglei53</li>
      <li>fenglei54</li>
      <li>fenglei55</li>
      <li>fenglei56</li>
      <li>fenglei57</li>
      <li>fenglei58</li>
      <li>fenglei59</li>
      <li>fenglei60</li>
      <li>fenglei61</li>
      <li>fenglei62</li>
      <li>fenglei63</li>
      <li>fenglei64</li>
      <li>fenglei65</li>
      <li>fenglei66</li>
      <li>fenglei67</li>
      <li>fenglei68</li>
      <li>fenglei69</li>
      <li>fenglei70</li>
      <li>fenglei71</li>
      <li>fenglei72</li>
      <li>fenglei73</li>
      <li>fenglei74</li>
      <li>fenglei75</li>
      <li>fenglei76</li>
      <li>fenglei77</li>
      <li>fenglei78</li>
      <li>fenglei79</li>
      <li>fenglei80</li>
      <li>fenglei81</li>
      <li>fenglei82</li>
      <li>fenglei83</li>
      <li>fenglei84</li>
      <li>fenglei85</li>
      <li>fenglei86</li>
      <li>fenglei87</li>
      <li>fenglei88</li>
      <li>fenglei89</li>
      <li>fenglei90</li>
      <li>fenglei91</li>
      <li>fenglei92</li>
      <li>fenglei93</li>
      <li>fenglei94</li>
      <li>fenglei95</li>
      <li>fenglei96</li>
      <li>fenglei97</li>
      <li>fenglei98</li>
      <li>fenglei99</li>
      <li>fenglei100</li>
    </div>
  </div>
</template>

<script>
import BScroll from 'better-scroll';

export default {
  name: 'Category',
  data() {
    return {
      scroll: null
    }
  },
  mounted() {
    this.scroll = new BScroll('.wrapper',{
      probeType: 3
    });
    this.scroll.on('scroll', (position) => {
      console.log(position);
    });
  },
  methods: {
    btnClick() {
      console.log('btnClick');
    }
  }

};
</script>

<style scoped>
  .wrapper {
    height: 150px;
    background-color: red;
    overflow: hidden;
    /* overflow-y: scroll; */
  }
</style>
