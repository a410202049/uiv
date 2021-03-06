<template>
  <section class="container-fluid">
    <div class="row">
      <div class="col-xs-12">
        <anchor-header text="Popover" source-folder="popover"></anchor-header>
      </div>
    </div>
    <div class="row">
      <div class="col-xs-12">
        <div>
          <popover :title="title"
                   :placement="placement"
                   :auto-placement="autoPlacement"
                   :trigger="trigger"
                   :enable="enable"
                   v-model="open1"
                   ref="popover">
            <button type="button" class="btn btn-default" data-role="trigger">Dynamic Popover</button>
            <div slot="popover">
              <h1>Hello world!</h1>
            </div>
          </popover>
          <popover :title="title"
                   :placement="placement"
                   :auto-placement="autoPlacement"
                   :trigger="trigger"
                   v-model="open2"
                   :enable="enable">
            <button type="button" class="btn btn-default" data-role="trigger">Functional Popover</button>
            <div slot="popover">
              <form>
                <div class="form-group">
                  <label>Title</label>
                  <input type="text" class="form-control" v-model="title">
                </div>
              </form>
            </div>
          </popover>
        </div>
        <br/>
        <div class="well">
          <form class="form-horizontal">
            <div class="form-group">
              <div class="col-md-3 col-sm-6">
                <label>Enable / Disable Popover</label>
                <div class="checkbox">
                  <label>
                    <input type="checkbox" v-model="enable"> Enable
                  </label>
                </div>
              </div>
              <div class="col-md-3 col-sm-6">
                <label>Auto Adjust Placement</label>
                <div class="checkbox">
                  <label>
                    <input type="checkbox" v-model="autoPlacement"> Enable
                  </label>
                </div>
              </div>
              <div class="col-md-6">
                <label>Title</label>
                <input type="text" class="form-control" v-model="title">
              </div>
            </div>
            <div class="form-group">
              <div class="col-md-6">
                <label>Placement</label>
                <select class="form-control" v-model="placement">
                  <option>top</option>
                  <option>right</option>
                  <option>left</option>
                  <option>bottom</option>
                </select>
              </div>
              <div class="col-md-6">
                <label>Trigger</label>
                <select class="form-control" v-model="trigger">
                  <option>hover</option>
                  <option>focus</option>
                  <option>hover-focus</option>
                  <option>click</option>
                  <option>outside-click</option>
                  <option>manual</option>
                </select>
                <div v-show="trigger === 'manual'">
                  <br/>
                  <button class="btn btn-default" @click="open1 = !open1">
                    <span>Toggle Popover 1</span>
                  </button>
                  <button class="btn btn-default" @click="open2 = !open2">
                    <span>Toggle Popover 2</span>
                  </button>
                </div>
              </div>
            </div>
          </form>
        </div>
      </div>
    </div>
    <div class="row">
      <div class="col-xs-12">
        <demo-code-block demo-file="PopoverDoc.vue">
        <pre><code>
&lt;popover title=&quot;Popover Title&quot;&gt;
  &lt;button type=&quot;button&quot; class=&quot;btn btn-default&quot; data-role=&quot;trigger&quot;&gt;Popover Trigger&lt;/button&gt;
  &lt;div slot=&quot;popover&quot;&gt;
    &lt;h1&gt;Hello world!&lt;/h1&gt;
  &lt;/div&gt;
&lt;/popover&gt;
        </code></pre>
        </demo-code-block>
      </div>
    </div>
    <div class="row">
      <div class="col-xs-12">
        <h3 class="page-header">API</h3>
        <h4>Note</h4>
        <ul>
          <li>
            <p>The element attached with <code>data-role="trigger"</code> will be the popover trigger.</p>
          </li>
        </ul>
        <h4>Props</h4>
        <ul>
          <li>
            <p>
              <code>tag: String</code>
              <span>The HTML tag that render the component. Default: 'span'.</span>
            </p>
          </li>
          <li><p><code>v-model: Boolean</code> Show / hide the popover.</p></li>
          <li><p><code>title: String</code> The popover title.</p></li>
          <li><p><code>enable: Boolean</code> Enable the popover. Default: true.</p></li>
          <li>
            <p>
              <code>placement: String</code>
              The popover placement, support top / bottom / left / right. Default: top.
            </p>
          </li>
          <li>
            <p>
              <code>auto-placement: Boolean</code>
              Try to auto adjust the content placement if the set one does not have enough space to show. Try order:
              top -> right -> bottom -> left, and use the set one if none of these matched. Default: true.
            </p>
          </li>
          <li>
            <p>
              <code>trigger: String</code>
              The popover trigger event, support:
            </p>
            <ul>
              <li><p>hover -> show on mouseenter, hide on mouseleave</p></li>
              <li><p>focus -> show on focus, hide on blur</p></li>
              <li><p>hover-focus -> combination of hover and focus trigger</p></li>
              <li><p>click -> toggle on trigger click</p></li>
              <li><p>outside-click -> same as click, but not close on popover click and close on outside click
                (Default)</p></li>
              <li><p>manual -> do not add event listeners, and controls only by v-model change</p></li>
            </ul>
          </li>
          <li><p><code>append-to: String</code> Element selector that the popover append to. Default: body.</p></li>
          <li>
            <p>
              <code>transition-duration: Number</code>
              The popover show / hide transition time in ms. Default: 150.
            </p>
          </li>
        </ul>
        <h4>Slots</h4>
        <ul>
          <li><p><code>popover</code> Replace as the popover body.</p></li>
          <li><p><code>default</code> Replace as the rest of the component (e.g. trigger stuffs).</p></li>
        </ul>
        <h4>Events</h4>
        <ul>
          <li><p><code>popover-show</code> Fire after popover show.</p></li>
          <li><p><code>popover-hide</code> Fire after popover hide.</p></li>
        </ul>
      </div>
    </div>
  </section>
</template>

<script>
  import AnchorHeader from '../architecture/AnchorHeader.vue'
  import DemoCodeBlock from '../architecture/DemoCodeBlock.vue'
  import Popover from '../../components/popover/Popover.vue'
  import hljsMixin from './../mixins/hljsMixin'
  export default {
    mixins: [hljsMixin],
    components: {AnchorHeader, DemoCodeBlock, Popover},
    data () {
      return {
        enable: true,
        title: 'Popover Title',
        trigger: 'outside-click',
        placement: 'top',
        autoPlacement: true,
        open1: false,
        open2: false
      }
    },
    methods: {}
  }
</script>

<style lang="less" rel="stylesheet/less" scoped>

</style>
